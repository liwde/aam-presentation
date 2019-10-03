# Die Software

Notes:
- Wir sahen: Wie kann so eine Software aussehen
- Jetzt: Warum ist es so, wie es ist?
- Und: Wie haben wir das angestellt?

---

## Warum nicht Excel?

Note: Come On, es ist Excel... macht so sau kein Bock damit zu arbeiten, außer man ist fresher Consultant bei KPMG

----

![Symbolbild Pflege in Excel](img/Excell_Beispiel_Anonymisiert.PNG)

----

- Beschränkte Funktionalität <!-- .element: class="bigger" -->
- Paralleles Pflegen mehrerer Listen <!-- .element: class="bigger fragment" -->
- Zugriffsprobleme und Versionierungsfrage <!-- .element: class="bigger fragment" -->
- Es ist Excel! <!-- .element: class="huge bold fragment" -->

Note:
- Zugriff und Versionierung: Insbesondere bei verteiltem Zugriff
- Daher: Andere Architektur nötig! Und die kommt jetzt.

---

## Architektur-Überblick

----

### Requirements

- plattformunabhängig <!-- .element: class="fragment" -->
- offlinefähig <!-- .element: class="fragment" -->
- einfache Benutzbarkeit <!-- .element: class="fragment" -->

----

### Technologie

<table class="clear centered padded">
    <tr>
        <td><img src="img/docker.png" height="200px" class="fragment" data-fragment-index="5"></td>
        <td><img src="img/couchdb_logo.png" height="200px" class="fragment" data-fragment-index="3"></td>
        <td><img src="img/pouchdb_logo.svg" height="200px" class="fragment" data-fragment-index="4"></td>
    </tr>
    <tr>
        <td><img src="img/html_logo.png" height="200px" class="fragment" data-fragment-index="1"></td>
        <td><img src="img/css_logo.svg" height="200px" class="fragment" data-fragment-index="1"></td>
        <td><img src="img/angular_logo.svg" height="200px" class="fragment" data-fragment-index="2"></td>
    </tr>
</table>

----

<!-- .slide: class="bigger" -->

### Funktionen

- Zentralisiertes Datenmanagement
- Einfacher Informationsaustausch
- Monitoring-Dashboard

---

## OR-Mapping

- EntityMapperService
- EntitySchemaService

----

### The Entity Model

![Entity Model](img/entity_relation.png)

----

### OR-Mapping / Entity-Document-Mapping

![OR-Mapping](img/or_mapping.png)

----

### Example Entity with Decorators

```ts
@DatabaseEntity('Child')
export class Child extends Entity {

    @DatabaseField() name: string;
    @DatabaseField() projectNumber: string;
    @DatabaseField({dataType: 'string'}) gender: Gender;
    @DatabaseField() dateOfBirth: Date;
    @DatabaseField() motherTongue = '';
    @DatabaseField() religion = '';
```

----

### OR-Mapping / Entity-Document-Mapping

```ts
public async save<T extends Entity>(entity: T, forceUpdate: boolean = false): Promise<any> {
    const rawData = this.entitySchemaService.transformEntityToDatabaseFormat(entity);
    const result = await this._db.put(rawData, forceUpdate);
    if (result.ok) {
        entity._rev = result.rev;
    }
    return result;
}
```

---

## Session-Management
- Offlinefähiger Login
- Synchronisierte Datenhaltung

Note:
- Verteiltes System
- Datenbank CouchDB -- synchronisiert
- --> Wie stellen wir da jetzt sicher, dass die Session stabil ist?
- Erste Frage: Wie sehen denn da die Zustände aus?

----

### State

![Session State](img/session_state.png)

Notes:
3 separate Status:
- `LoginState`: Unabhängig von Netzwerk: "Bin ich eingeloggt?"
- `ConnectionState`: Wie ist die Verbindung zur entfernten Datenbank?
- `SyncState`: Wie ist die Synchronisation?

----

![Session Classes](img/session_classes.png)

Notes:
- Oben: Entities aus dem OR Mapper
- Session: In zwei Bestandteile gespalten
- Datenbank per Provider aus der Session
- Das coole: Anderer Provider --> andere Session --> andere Datenbank --> Mockdaten!
- Mehr Details: Code! Gut dokumentiert, wie das asynchron gehandhabt wird

---

## Repsonsive Design

- Flex Design
- Breakpoints & Listener

Notes:
Demo after Attendance Register

----

<!-- .slide: data-background-iframe="https://demo.aam-digital.com" data-background-interactive -->

---

## Attendance Register

Eine einfache Wizard-Anwendung die alles kombiniert

Notes:
Demo time!

----

<!-- .slide: data-background-iframe="https://demo.aam-digital.com" data-background-interactive -->
