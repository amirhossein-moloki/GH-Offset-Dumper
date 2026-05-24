# **Guided Hacking Offset Dumper**

[**Persian Documentation (فارسی)**](README_FA.md)

A professional-grade, modernized signature scanner and offset dumper for games. This tool rapidly generates C++ headers, Cheat Engine tables, and ReClass.NET projects for any game, supporting both runtime memory scanning and disk-based analysis.

![image](resources/code.png)

## **Key Features**
- **Cheat Table Generation (.ct):** Automatically creates organized tables with Local Player and Entity List structures.
- **ReClass.NET Support (.rcnet):** Converts netvar tables into ReClass.NET classes with appropriate data types.
- **C++ Header Output (.hpp):** Generates clean, ready-to-use headers for your hacking projects.
- **On-Disk Dumping:** Scan binary files directly without needing to run the game.
- **Netvar Dumping:** Built-in support for Source Engine games to extract network variables.
- **JSON-Driven Configuration:** Easily manage multiple games and projects using simple JSON files.

---

## **Full Usage Guide**

### **1. Prerequisites**
- **Visual Studio 2022** (with "Desktop development with C++" workload).
- **CMake** (optional, for VS Code or CLI builds).

### **2. Installation**
Clone the repository to your local machine:
```bash
git clone https://github.com/GuidedHacking/GH-Offset-Dumper.git
cd GH-Offset-Dumper
```

### **3. Building the Project**
#### **Visual Studio:**
1. Open `GH-Offset-Dumper.sln`.
2. Set the build configuration to **Release** and select the appropriate platform (**x64** or **x86**) matching your target game.
3. Select **Build > Build Solution**.

#### **VS Code:**
1. Install **C/C++** and **CMake Tools** extensions.
2. Open the project folder.
3. Select the `Visual Studio Community 2022 Release - amd64` kit.
4. Build using the CMake extension.

### **4. Configuration**
The dumper relies on JSON files. A sample is provided in `configs/config.json`. You define your signatures and netvars here.

**Note:** Always use the dumper version that matches the game's architecture (64-bit dumper for 64-bit games).

### **5. Running the Dumper**

#### **Runtime Mode (Scanning an active game):**
1. Launch the game.
2. Drag and drop your `config.json` (or any custom JSON config) onto the `GH-Offset-Dumper.exe`.
3. The results will be saved in a new folder named after your configuration's `filename`.

#### **Disk Mode (Scanning without running the game):**
1. Set `"fileonly": true` in your JSON config.
2. Provide the path to the game binary in `"exefile"`.
3. Drag and drop the config onto the dumper.

### **6. Output Files**
The tool generates a directory containing:
- `offsets.hpp`: The C++ header for your source code.
- `offsets.ct`: A ready-to-use Cheat Engine table.
- `offsets.rcnet`: A ReClass.NET project file.

---

## **JSON Configuration Reference**

```json
{
  "executable": "game.exe",           // Target process name
  "filename": "MyGame_Offsets",       // Output directory name
  "signatures": [
    {
      "name": "dwLocalPlayer",        // Offset name
      "pattern": "8D 34 85 ? ? ? ? 89 15 ? ? ? ? 8B 41 08 8B 48 04 83 F9 FF",
      "module": "client.dll",         // Target module
      "relative": true,               // Result relative to module base
      "extra": 3                      // Constant to add to result
    }
  ],
  "netvars": [                        // Source Engine specific
    {
      "name": "m_iHealth",
      "table": "DT_BasePlayer",
      "prop": "m_iHealth"
    }
  ]
}
```

---

## **Troubleshooting**
- **Process Not Found:** Ensure the game is running and you have Administrator privileges.
- **Pattern Not Found:** The signature might be outdated. Check GuidedHacking for updated patterns.
- **Architecture Mismatch:** Ensure you are using the correct dumper architecture (x86/x64).

---

## **Credits & Education**
Developed by Guided Hacking. For professional game hacking courses, visit [GuidedHacking.com](https://guidedhacking.com).

*Special thanks to contributors of hazedumper, nlohmann-json, and base64 libraries.*
