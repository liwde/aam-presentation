# Die Software

---

## Warum nicht Excel?

Note: Come On, es ist Excel... macht so sau kein Bock damit zu arbeiten, außer man ist fresher Consultant bei KPMG

----

### Beispiel 

<img src="img/Excell_Beispiel_Anonymisiert.PNG">

----

<ul>
    <li>Beschänkte Funktionalität</li>
    <li>Paralleles Pflegen mehrer Listen</li>
    <li>Zugriffsprobleme und Versionierungsfrage bei verteiltem Zugriff</li>
    <li>Es ist Excell!</li>
</ul>

---

## Architektur-Überblick

---

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
