# KQders Auction (Fabric client mod)

Client-side auction builder, live HUD overlay, winner recording and history for Minecraft 1.21.4 (Fabric).

## Build
1. Install JDK 21.
2. In this folder run `gradle wrapper --gradle-version 8.12` once (needs Gradle installed), or open the folder in IntelliJ IDEA and let it import the Gradle project.
3. `./gradlew build` -> the mod jar is in `build/libs/kqders-auction-1.0.0.jar` (not the `-sources` one).
4. Put the jar in `.minecraft/mods` with Fabric Loader and Fabric API for 1.21.4.

To target another Minecraft version, copy the matching values from https://fabricmc.net/develop into `gradle.properties`. Newer versions changed some GUI/HUD/keybind APIs, so the code may need small edits.

## Default keys (rebindable under Controls > KQders Auction)
K open builder | [ start/pause | ] cancel (or dismiss finished result) | \ copy winner | ; record-winner screen

## How winners work
- The timer reaching 0 only moves the lot to "Time up". It is never marked Sold automatically.
- You type the winner's username and the amount they paid, then press SET WINNER. Payments below the minimum are rejected.
- COPY WINNER USERNAME puts exactly the username on the clipboard.
- Chat integration: the mod watches *system* chat messages for lines like `Steve paid you $5,000`. Matches appear in the Record Winner screen as clickable suggestions. They never set a winner and are not payment verification. The pattern is the `paymentRegex` field in `config/kqders_auction.json` (needs named groups `player` and `amount`). Player-typed chat is ignored unless you set `listenPlayerChat` to true, because anyone can fake those lines.

## Data
`config/kqders_auction.json` stores owner name (default KQders), your draft, presets, history, chat settings and `hudScale`.
