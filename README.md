Here is one of my Python scripts, designed to capture and dump TCP traffic for games running over OpenVPN/TUN0. It includes 55 filters covering popular games, gaming platforms, communication services, and common multiplayer protocols.

The script is designed to help identify traffic associated with specific games and services. For peer-to-peer (P2P) traffic, rather than traffic going through dedicated servers, relevant connection information may be observable through the VPN interface.

IP/API and Filtering System

The script uses a custom API for IP information, together with an IP table and filtering system. The filters are designed to help distinguish gaming/P2P traffic from traffic belonging to major cloud providers and infrastructure services.

It also includes exclusion rules for infrastructure associated with services such as Cloudflare, Rockstar, and other major cloud/hosting providers, helping reduce unrelated traffic and potential false positives.

Dedicated Servers and P2P Fallbacks

Although the main focus is identifying P2P traffic, I have also included filters for some dedicated-server-based games and services.

The reason for this is that some games and applications can use a hybrid networking model. A game may normally use dedicated servers but switch or supplement the connection with P2P networking in certain situations, such as private matches, player-hosted sessions, voice communication, connection fallback, or other networking scenarios.

Because of this, filtering only for known P2P titles would potentially miss some traffic. The additional dedicated-server filters are intended to provide broader coverage and make it easier to identify traffic when a game changes how it establishes connections.

The filters should therefore be treated as traffic-identification patterns rather than guaranteed indicators of a specific game or player. The actual networking behavior can vary depending on the game mode, platform, region, NAT configuration, server availability, and the game's current networking architecture.

Available Filters

The current filter list includes:

#	Filter
1	Facebook/Meta Call
2	WhatsApp Call
3	Discord Voice
4	PlayStation Party
5	Xbox Multiplayer
6	PlayStation Multiplayer
7	Nintendo Online
8	Black Ops 2 Zombies
9	Call of Duty Multiplayer
10	Black Ops 3 Zombies
11	Black Ops 3 Multiplayer
12	Steam/Valve Games
13	Steam P2P
14	Source Engine
15	Minecraft Server
16	Minecraft Bedrock
17	Battlefield
18	EA Sports FC / FIFA
19	EA P2P
20	Rocket League
21	Rust
22	Valheim
23	Terraria
24	Factorio
25	Quake
26	Broad UDP Games
27	Broad TCP Games
28	ARK: Survival Evolved
29	ARK: Survival Ascended
30	Fortnite
31	Apex Legends
32	Valorant
33	GTA Online / FiveM
34	Rainbow Six Siege
35	PUBG
36	Destiny 2
37	Sea of Thieves
38	Palworld
39	Enshrouded
40	DayZ / Arma
41	Project Zomboid
42	7 Days to Die
43	Conan Exiles
44	Don't Starve Together
45	Stardew Valley
46	Dead by Daylight
47	Phasmophobia
48	Sons of the Forest
49	V Rising
50	Helldivers 2
51	League of Legends
52	Overwatch
53	War Thunder
54	No Man's Sky
55	Fallout 76
Usage
python3 vpn_pullerv2.py <ip>


The script was created by me with assistance from various GPT jailbreak techniques. It can also be run in Docker, although I have found that setup to be less effective.

The script is primarily designed for Linux and is intended to run on a VPS using OpenVPN while monitoring traffic associated with connected VPN clients.

VPS and SSH Support

When the script is installed on a VPS, it can also be used remotely through SSH. I set mine up with a forced SSH command and wrapper menu, allowing the application to launch automatically when connecting over SSH rather than requiring the user to manually navigate to the script.

This makes the interface usable from practically any SSH client, including phones and tablets.

The SSH wrapper can be configured to:

Launch the menu automatically after authentication.

Provide access to the available traffic filters.

Select the client IP to monitor.

Start and stop monitoring functions.

Run the relevant Python functions without exposing a normal shell.

Work with mobile SSH applications.

Custom Banner Support

The SSH interface also supports an optional banner.py file. If you add banner.py in the appropriate location within the project, it can be loaded by the wrapper and used to display a custom banner when the menu starts.

This can be useful for adding a project name, version information, system information, or other custom terminal UI elements.

PC and Console Setup

The filters work natively when the game is running on a PC.

For consoles, the console's traffic generally needs to be routed through a PC or VPN router. There are several possible setups:

Wi-Fi hotspot: Share the PC's VPN connection with the console.

Ethernet: Connect the console to the PC and share the VPN connection.

VPN router: Install the OpenVPN .ovpn configuration on a compatible VPN router.

A VPN router can be particularly convenient when multiple devices are involved because the devices can connect to the router over Wi-Fi and use the VPN connection without individually configuring each device.

Examples

I have also included several examples showing how the filters and networking detection work in different situations. These examples are intended to demonstrate the type of traffic the script can identify and how the results can differ depending on whether a connection is using P2P, dedicated infrastructure, or a fallback networking method.

I have added the examples alongside the project so they can be reviewed together with the corresponding filters and configuration.

Important Limitations

The script is primarily useful for traffic that can actually be observed through the VPN interface. Games using dedicated servers, cloud infrastructure, relays, NAT traversal, or encrypted/obfuscated networking may not expose useful peer information.

The IP/API filtering system is intended to reduce infrastructure-related false positives, but it cannot guarantee that every detected connection belongs to a particular game or player. Networking behavior can also change between game modes, updates, platforms, and regions.
