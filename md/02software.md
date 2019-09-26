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

### TecStack Backend

<table class="clear centered padded">
    <tr>
        <td><img src="img/nodejs_logo.png" height="200px"></td>
        <td><img src="img/couchdb_logo.png" height="200px"></td>
        <td><img src="img/pouchdb_logo.svg" height="200px"></td>
    </tr>
    <tr style="font-size: 10px">
        <td>Node.js</td>
        <td>CouchDB</td>
        <td>PouchDB</td>
    </tr>
</table>

----

### TecStack Frontend

<table class="clear centered padded">
    <tr>
        <td><img src="img/html_logo.png" height="200px"></td>
        <td><img src="img/css_logo.svg" height="200px"></td>
        <td><img src="img/angular_logo.svg" height="200px"></td>
    </tr>
    <tr style="font-size: 10px">
        <td>HTML</td>
        <td>CSS</td>
        <td>ANGULAR</td>
    </tr>
</table>

## Session-Management

- PouchDB

----

### State

![Session State](img/session_state.png)

----

### Classes

![Session Classes](img/session_classes.png)

----

### Code

```ts
public login(username: string, password: string): Promise<LoginState> {
    const localLogin =  this._localSession.login(username, password);
    const remoteLogin = this._remoteSession.login(username, password);
    remoteLogin.then(async (connectionState: ConnectionState) => {
        // remote connected -- sync!
        if (connectionState === ConnectionState.connected) {
            const syncPromise = this.sync();
            // no liveSync() here, as we can't know when that's finished if there are no changes.
            // ...
        }
    });
}
```

---

## OR-Mapping

- EntityMapperService <!-- .element: class="fragment" data-fragment-index="1" -->
- EntitySchemaService <!-- .element: class="fragment" data-fragment-index="2" -->

----

### The Entity Model

![Entity Model](img/entity_relation.png)

----

### OR-Mapping / Entity-Document-Mapping

![OR-Mapping](img/or_mapping.png)

---

## Repsonsive Design

- Flex Design
- Breakpoints & Listener

---

## Attendance Register

Eine einfache Wizard-Anwendung die alles kombiniert
