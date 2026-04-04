# TOTAL SOURCE SUPPORT!

### 18K Tracked Convicts!

# Synapse AntiCheat
> In Development, Do not expect a release anytime soon

**Bleeding-edge automated cheat detection & launcher for Source Games**

SAC is an attempt at an advanced automated system that analyzes gameplay to detect cheaters in real-time with high accuracy with a community database  
It identifies cheat patterns and known bad actors to keep your games clean!  
Synapse also serves as a comprehensive launcher with all known launch arguments pre-configured and ready to customize.

![Status](https://img.shields.io/badge/status-Early%20Alpha-green)

> **⚠️ Important:** Synapse IS NOT PUBLIC YET, Stop downloading malware!

---

## 🎯 Features

### Automated Detection Engine
- **Real-time replay analysis** - No second instance required by default!
- Multi-method detection system with comprehensive cheat coverage
- Confidence-based rating system verified through human review
- Automatic reporting with demo file evidence

### Integrated Game Launcher
- **All known launch arguments** pre-configured and ready to use
- **Automatic configuration** of required settings for Synapse
- **User-customizable** launch options for personal preference
- **One-click launch** straight in with optimal settings

---

### Integrated Database Systems

<details>
<summary><b>TF2 Supported External Databases</b></summary>

- **MegaAntiCheat (MAC)** - Utilize MAC's database with your masterbase key
- **TF2BD Playerlists** - Import and use existing TF2 Bot Detector lists and rulesets
- **SteamHistory API** - Enhanced user tracking (requires API key)
  - Provides SourceBans integration automatically
  - Shows SourceMod AntiCheat bans
  - Keyword-based flagging
- **Steam Web API** - Two methods available:
  - RCON-based data gathering (TF2BD-style)
  - Steam Web API key (recommended)
- **Reputation Sites** - Used to determine priority checking for users

</details>

### Smart User Verification

<details>
<summary><b>Account Analysis Factors</b></summary>

- **VAC/Game Ban Assessment**
  - Recent bans: Higher scrutiny
  - 5+ years: Not automatically checked
  - 10+ years: Considered irrelevant
  - VAC bans never result in auto-conviction (could be false positives like ReShade)
  - Game bans only counted on suspected users (developers can issue arbitrary bans)
  
- **Account Age Checking**
  - Identifies potential alt accounts
  - Only flags when suspicious behavior is present
  - New players are not automatically flagged

- **Reputation Analysis**
  - Profile comments analyzed for keywords and patterns
  - Only counted when sufficiently negative or suspicious
  - Not weighted heavily due to abuse potential

</details>

### User Classification System

- **Convicted** - Confirmed cheaters with labeled detection methods
- **Suspicious** - Marked during active analysis by the replay analyzer
- **Advise** - Flagged for manual community review
- **Clean** - No suspicious activity detected

### Automated Response Actions

- **Auto-kick** - Automatically removes convicted cheaters and bots
- **Chat Alerts** - Notifies other players of convicted cheaters
- **Evidence Submission** - Automatic demo file reporting
- **Blacklist Sync** - Real-time synchronization with master database

---

## 💻 System Requirements

### Supported Platforms
- ✅ Linux
- ✅ MacOS
- ✅ Windows

### Hardware Requirements

**Standard Setup:**
- **CPU:** Multi-core processor recommended
- **RAM:** 8GB+ recommended
- **Storage:** Space for demo file storage

**Optional: Offload Analysis to Secondary System**
Want maximum performance on your main gaming machine? You can optionally leverage a spare system on your local network to handle replay analysis:
- Second computer on the same local network or "local" meshes
- Synapse provides everything needed for setup
- Keeps your gaming system at peak performance
- Analysis workload completely offloaded

---

## 🚀 How It Works

1. **Launch Synapse** - Synapse serves as your game launcher with optimized settings
2. **Game Monitoring** - Synapse connects to your instance via RCON
3. **Replay Analysis** - Advanced analyzer processes gameplay in real-time (on your machine or optional secondary system)
4. **Multi-Database Checking** - Cross-references players against multiple databases
5. **Detection Engine** - Analyzes gameplay for known cheat signatures and suspicious patterns
6. **Classification** - Players are marked as convicted, suspicious, or clean
7. **Automated Actions** - Kicks, reports, and alerts based on detections
8. **Community Sync** - Convicted cheaters (only those detected by Synapse) are synced to master database

---

## 📋 Installation

### Prerequisites
- Any Source Game with RCON
- RCON access (Synapse provides setup instructions if connection fails)

### Optional API Keys (Recommended)
- MegaAntiCheat masterbase key
- SteamHistory API key
- Steam Web API key

### Quick Start

<details>
<summary><b>Installation Steps</b></summary>

1. Download the latest release from the releases page
2. Extract to your preferred location
3. Run Synapse AntiCheat
4. Configure RCON connection (Synapse will guide you)
5. Optionally add API keys for enhanced functionality
6. Start playing!

Synapse can:
- **Automatically connect to your games** - Links to your running game instance
- **Guide RCON setup** - Provides instructions without requiring game restart
- **Import existing lists** - Load exiting lists from various providers (TF2 Mainly)

</details>

---

## ⚙️ Configuration

<details>
<summary><b>API Keys Configuration</b></summary>

### MegaAntiCheat Integration
1. Obtain your masterbase key from MegaAntiCheat
2. Enter in Synapse settings
3. Database will sync automatically

### Steam API Setup
1. Get your API key from https://steamcommunity.com/dev/apikey
2. Add to Synapse configuration
3. Enhanced user lookup enabled

### SteamHistory API
1. Request API key from SteamHistory
2. Configure in settings
3. Advanced tracking features unlocked

</details>

<details>
<summary><b>Import Existing Data</b></summary>

### TF2BD Playerlists
- Import your existing player lists
- Maintain your custom rulesets
- Seamless transition from TF2BD

### SourceBans Integration
- Automatically configured
- Checks for SourceMod AntiCheat bans
- Keyword-based ban detection

</details>

---

## 🛡️ Detection Philosophy & Accuracy

### Our Approach

<details>
<summary><b>What We Consider</b></summary>

✅ **Used as Evidence:**
- Replay analysis results
- Multiple suspicious behavior patterns
- Cross-database verification
- Statistical anomalies
- Movement and aim patterns

❌ **What We DON'T Auto-Convict On:**
- VAC bans alone (too many false positives, e.g., ReShade)
- Game bans alone (can be arbitrary)
- 3rd Party Listings alone (not curated by us)
- Inventory value (cheaters use expensive items to appear legit)
- Reputation sites alone (easily manipulated)
- Account age alone (new players aren't cheaters by default)

</details>

<details>
<summary><b>Confidence Rating System</b></summary>

Our confidence ratings are based on:
- Confirmed convictions from our detection engine
- Human review of replay footage
- Cross-validation with multiple detection methods
- Community feedback and manual reviews

**Important Notes:**
- 3rd Party convictions strengthen our analysis but don't result in auto-conviction
- We only sync users that **Synapse itself** has convicted to our database
- Manual markings are **NOT** synced to prevent abuse
- Users can share custom lists, but these should be taken with a grain of salt

</details>

---

## 🚫 Blacklist Policy

<details>
<summary><b>Important Information</b></summary>

**Blacklisted users CANNOT use Synapse.** 

This is a permanent restriction because:
- We don't want cheaters using our software
- We don't want them using it against others
- Blacklist decisions are final and irreversible

**Technical Implementation:**
- We detect blacklisted users by our own metrics
- Local countermeasures are placed on the system upon detection
- Once detected, the system stays detected (cannot be bypassed)
- **Zero tolerance policy:** If we detect a cheat injected while using Synapse, you will be automatically convicted AND blacklisted
- We will NOT disclose how we detect injected cheats or blacklisted users

**If you've been blacklisted:**
- You cannot appeal through normal channels
- You cannot create new accounts to bypass

</details>

---

## 📊 Performance & Accuracy

- **Active Development** - Continuously improving detection algorithms
- **Community-Driven** - Accuracy improves as more users contribute data
- **Human-Verified** - Confidence ratings validated through manual review
- **Multi-Source Validation** - Cross-references multiple databases and detection methods

---

## 🔒 Privacy & Data Collection

**We respect your privacy.** Synapse does NOT collect any account information whatsoever.

<details>
<summary><b>What We Collect</b></summary>

**The ONLY data we collect:**
- ✅ Conviction data (cheaters detected by Synapse)
- ✅ Player markings from replay analysis

**What we DON'T collect:**
- ❌ Your Steam account information
- ❌ Personal data
- ❌ Chat logs
- ❌ Game settings or preferences
- ❌ System information
- ❌ Location data
- ❌ Any identifying information beyond Steam IDs in convictions

</details>

<details>
<summary><b>Replay Analysis & Opt-Out</b></summary>

**All replay analysis is done ON YOUR MACHINE.**

- No replay data is sent to our servers
- Analysis happens locally using your hardware
- You maintain complete control

**Want to opt out of being an analyst?**
Simply disable replay analysis in settings. You'll still benefit from the community database, but your system won't contribute analysis data.

</details>

---

## 🤝 Community Features

- **Shared Blacklist** - All users benefit from centralized cheater database (Synapse-convicted only)
- **Conviction Labels** - See exactly what cheats each player was caught using
- **Manual Review System** - Submit edge cases for community analysis
- **Evidence Storage** - Automatic demo file preservation and reporting
- **Chat Integration** - Alert other players to convicted cheaters
- **Hive Network** - Link multiple Synapse instances together!
  - Perfect for LAN parties or networked play
  - Works over local networks or via Tailscale/similar
  - Share a single analyst system across multiple users
  - Automatically prompted when Hive is enabled
  - All connected users benefit from shared analysis power

---

## ⚠️ Important Notes & Disclaimers

<details>
<summary><b>About Inventory Value</b></summary>

**We do NOT account for inventory value.** Cheaters frequently use expensive items (Unusual hats, Australium weapons, etc.) to appear more legitimate. A valuable backpack is not evidence of innocence.

</details>

<details>
<summary><b>About Reputation Sites</b></summary>

Profile reputation and comments are only considered when:
- Sufficiently negative ratings exist
- Multiple suspicious keywords are found in comments
- Used as supporting evidence, never primary evidence

Reputation can be easily manipulated and is not reliable as a primary indicator.

</details>

<details>
<summary><b>About VAC & Game Bans</b></summary>

**VAC Bans:**
- Permanent bans for detected cheats
- We **never** auto-convict based solely on VAC bans
- Older bans may indicate reformed players
- False positives exist and are more common than people think:
  - **ReShade** - Graphics injector for visual enhancements
  - **Texture mods** - Custom skins and textures
  - **ENB Series** - Graphics enhancement suite
  - **SweetFX** - Post-processing injector
  - **Cheat Engine** - If left running in background (even unused)
  - **AutoHotkey scripts** - Macro tools for accessibility
  - **DLL injectors** - Even for legitimate modding purposes

**Game Bans:**
- Only counted on already-suspicious users
- Developers can issue arbitrary bans
- Do not constitute definitive proof of cheating

</details>

<details>
<summary><b>Responsibility & Liability</b></summary>

- Synapse is not responsible for abuse of the software
- Manually marked cheaters **will NOT** be synced to our database
- Only Synapse-detected convictions are shared
- User-shared lists should be treated as unverified
- Use responsibly and in accordance with server rules and Valve's Terms of Service

</details>

<details>
<summary><b>Platform Support Policy</b></summary>

**Officially Supported:**
- Linux

**Unsupported:**
- macOS (may work via Wine/Proton, but we provide no support)

We focus development on platforms we can properly test and support.

</details>

---

## 🏗️ Technical Details

- **Language:** Written entirely in C++
- **GUI Framework:** QT for native overlay interface
- **Architecture:** Replay analyzer for real-time detection (no second instance required!)
- **Platform Support:** Windows, MacOS, Linux

---

## 🔮 Roadmap

- [ ] Enhanced detection algorithms
- ✅ Improved heuristic patterns
- ✅ Additional cheat signature detection
- ✅ **Hive Network** - Multi-user instance linking
- [ ] Expanded community features
- [ ] Performance optimizations
- ✅ Advanced replay analyzer capabilities

---

## 🤔 FAQ

<details>
<summary><b>Do I have to use Synapse as my launcher?</b></summary>

No! Synapse can work with instances launched by any method. However, using Synapse as your launcher provides:
- Automatic configuration of required settings
- All known launch arguments pre-configured
- Easy customization of launch options
- One-click launch with optimal settings

You can still use Steam, shortcuts, or other launchers if you prefer.

</details>

<details>
<summary><b>Will this get me VAC banned?</b></summary>

No. Synapse AntiCheat does not modify game files or memory. It only analyzes demo files and RCON data, which are completely legitimate uses of Source's built-in features.

</details>

<details>
<summary><b>Can I use this on community servers?</b></summary>

Yes! Synapse is perfect for server administrators. It can automatically kick convicted cheaters, alert players via chat, and integrate with your existing ban systems.

</details>

<details>
<summary><b>Do I still need a second computer or instance?</b></summary>

No! Our new replay analyzer eliminates this requirement. Synapse now works seamlessly with just your main game instance.

</details>

<details>
<summary><b>What about false positives?</b></summary>

False positives are possible with any automated system. That's why we:
- Use confidence ratings
- Support manual review
- Cross-reference multiple databases
- Never auto-convict on single data points
- Allow community verification

</details>

<details>
<summary><b>Will my 3rd Party Lists work with Synapse?</b></summary>

Yes! Synapse can import and use playerlists and rulesets. These help strengthen our analysis but don't result in auto-convictions on their own.

</details>

<details>
<summary><b>I paid for Synapse. What should I do?</b></summary>

**You've been scammed!** Synapse isn't even public yet! Please:
1. Report the scam to us immediately
2. Request a refund/chargeback from your payment provider
3. Help us track down the scammer

</details>

<details>
<summary><b>Can I run Synapse in a Virtual Machine?</b></summary>

Absolutely! We fully support VM usage and encourage players to use whatever setup works best for them.

</details>

<details>
<summary><b>How do I get unbanned from Synapse?</b></summary>

If you believe you've been falsely convicted, you can attempt to initiate our **Redemption Process**:

**Eligible Reasons:**
- False conviction due to system error
- Compromised/hacked account (you were not in control)
- Other legitimate extenuating circumstances

**Process:**
1. Contact us with detailed evidence that you are not cheating
2. Provide context and proof (account security logs, etc.)
3. Our team will review your case

**If Pardoned:**
- You are completely wiped from our database
- It's as if you were never there
- Full restoration of access

This is NOT a guarantee - you must provide compelling evidence. Legitimate false convictions are taken very seriously.

</details>

<details>
<summary><b>What if I was using Synapse and got detected with a cheat?</b></summary>

**Zero tolerance.** If we detect a cheat has been injected while you're using Synapse:
- Automatic conviction
- Automatic blacklist
- No appeals
- Permanent ban from using Synapse

There is a reason we won't disclose how we do this, Cheat developers would just bypass it then.  
Nice try TT, but a sensible anticheat dev wouldn't just expose how to bypass their system.  
</details>

---

## 📜 License

As synapse will not be open sourced we have decided on a proper EULA and License.  
Yes it will be free, just not FOSS because it's an anticheat designed to stop cheaters.

**Remember:** Synapse is FREE SOFTWARE. Anyone charging for it is scamming you!

---

## 🙏 Contributing

We don't have a feasable way to safely open source this while being able to keep the system untampered  
Therefore we cannot allow open source contributions, instead we will encourage suggestions on release.  

---

## 📞 Support

<details>
<summary><b>Getting Help</b></summary>

Synapse hasn't released yet so this section is cleared for now.  

</details>

---

## 💬 A Message to Cheaters

**We're always watching.** 

You REALLY should of knew this was coming  
- 
Did you think i was foolish enough to just sit in the dark while you ruined my favorite game?  
No, instead I decided to take what I learned to develop a swiss army knife against you all.  
All of your "Undetected" softwares are *very easy* to detect with a little competence.  
This includes those of you making those "External Kernel Cheats"  
Take this as a warning, We only released a TF2BD list to track you.  
We're going to enjoy when the master list goes public with nearly 100k convicts.

---

## ⚖️ Final Disclaimer

**Use responsibly and in accordance with:**
- Server rules and policies
- Valve's Terms of Service
- Valve's community guidelines
- Local laws and regulations

We are not responsible for misuse of this software. Server administrators and users are responsible for ensuring their use complies with all applicable rules and regulations.

---

**Made with 🔧 for the gaming community**

*Keeping your games fair, one detection at a time.*
