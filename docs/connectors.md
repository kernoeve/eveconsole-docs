# Connectors (preview)

!!! warning "Preview"
    Connectors are a new interface with limited support for now. No connector has been released yet, so most people have nothing to set up here. Without one, EVE Console works exactly as before.

A **connector** is a separate program that links EVE Console to services your corporation or alliance runs, such as the site where members register their characters. You run it yourself, usually on the same PC, or your corporation or alliance may host one for its members. EVE Console never holds anyone else's EVE tokens: the connector answers its questions with what your group's services already have.

## What it is used for

So far EVE Console reads one thing from a connector: **linked characters**, which characters belong to one player. The other functions a connector can offer (auth groups, member and corporation ESI data, fleet participation) can be ticked and saved, but nothing uses them yet.

## Adding one

Open **Settings ▸ Connectors** and press **New connector**.

1. Enter the **Connector address**, for example `http://localhost:5054/`. Plain `http://` is allowed only for a connector on this PC; use `https://` for one anywhere else.
2. Press **Connect with EVE**. A page from the connector opens with a code. Check that it shows the same code EVE Console shows you, confirm it there, and sign in with EVE. Never confirm a code that EVE Console didn't show you.
3. Under **Used for**, tick the **Corporations** and **Alliances** of your characters it is for. A connector with none ticked isn't used.
4. Under **Functions**, tick **Linked characters**. Only what the connector offers can be ticked.

The connector's row then shows whether it is connected, and how many accounts and characters it linked, and when. **Refresh Now** asks it again; **Disconnect** ends its sign-in, and **Remove connector** forgets it and everything it gave.

## Several connectors

You can add several, for example when two of your corporations, or a corporation and an alliance, each run their own:

- Each is used only for the corporations and alliances chosen for it, and only for the functions ticked. It is never asked about anyone outside them.
- For a character, a connector chosen for its corporation comes before one chosen for its alliance.
- Two connectors can't have the same function for the same corporation or the same alliance: untick it on one first.
- Removing or disconnecting one clears only what it gave.

## On a shared database

On a [PostgreSQL](storage-postgresql.md) database shared by several PCs, the PC doing the [background work](background-processing.md) reads linked characters from each connector every half hour. Run the connector where the worker runs, or where every PC can reach it.

The connectors' keys are kept from the [AI agent](ai-agent-eden.md): it can't read them.

## Writing a connector

The interface belongs to EVE Console, and anyone can write a connector for their own group's services. The specification is in the app's repository: [`docs/connector/README.md`](https://github.com/kernoeve/EveConsole/blob/main/docs/connector/README.md), with the machine-readable [`openapi.yaml`](https://github.com/kernoeve/EveConsole/blob/main/docs/connector/openapi.yaml).
