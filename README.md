## Alias and Shortcut Bindings

### Line Commands

| Alias | Macro      |
|-------|------------|
| L     | '_Line     |
| SL    | '_Split    |
| TR    | '_Connect  |
| TT    | '_Trim     |

### View Commands

| Alias       | Macro                      | Shortcut |
|-------------|----------------------------|----------|
| H           | '_Hide                     |          |
| HI          | '_Isolate                  |          |
| LO          | '_OneLayerOff              |          |
| WW          | '_CPlane _World _Top       |          |
| ZS          | '_Zoom _Selected           |          |
|             | '_CPlane _Object           | Ctrl+D   |
|             | '_CPlane _World _Top       | Ctrl+1   |
|             | '_CPlane _World _Front     | Ctrl+2   |
|             | '_CPlane _World _Right     | Ctrl+3   |
|             | '_CPlane _World _Back      | Ctrl+4   |
|             | '_CPlane _World _Left      | Ctrl+5   |

### Transform Commands

| Alias  | Macro                                                      |
|--------|------------------------------------------------------------|
| M      | '_Move                                                     |
| E      | '_PushPull                                                 |
| EC     | '_ExtrudeCrv                                               |
| ES     | '_ExtrudeSrf                                               |
| E      | '_Explode                                                  |
| ESrf   | '_DupBorder _SelLast _PlanarSrf _SelPrev _Delete _SelLast  |
| P      | '_Planar                                                   |
| PC     | '_ProjectToCPlane _Yes                                     |
| PS     | '_PlanarSrf _SelLast _MergeAllEdges                        |
| J      | '_Join                                                     |
| JJ     | '_MergeAllCoplanarFaces                                     |
| JJJ    | '_MergeAllEdges                                            |

### Boolean Commands

| Alias  | Macro                                                      |
|--------|------------------------------------------------------------|
| BS     | '_BooleanSplit                                             |
| BU     | '_BooleanUnion _MergeAllEdges _MergeAllCoplanarFaces       |
| BD     | '_BooleanDifference                                        |


## RunPythonScripts

## Scripts

## Scripts

| Alias | Script Name                               | Command                                                   |
|-------|-------------------------------------------|-----------------------------------------------------------|
|       | ARI_BLOCK_SuperSelectBlocks               | ! _-RunPythonScript "X:\\...\\ARI_BLOCK_SuperSelectBlocks.py"               |
|       | ARI_CRV_SplitAllIntersections             | ! _-RunPythonScript "X:\\...\\ARI_CRV_SplitAllIntersections.py"             |
|       | ARI_GEO_CappedSlice                       | ! _-RunPythonScript "X:\\...\\ARI_GEO_CappedSlice.py"                       |
|       | ARI_GEO_Check                             | ! _-RunPythonScript "X:\\...\\ARI_GEO_Check.py"                             |
|       | ARI_GEO_CleanUnion                        | ! _-RunPythonScript "X:\\...\\ARI_GEO_CleanUnion.py"                        |
|       | ARI_LAYER_IFCandBeamLayers                | ! _-RunPythonScript "X:\\...\\ARI_LAYER_IFCandBeamLayers.py"                |
|       | ARI_OBJ_ObjMoveToLayerByType              | ! _-RunPythonScript "X:\\...\\ARI_OBJ_ObjMoveToLayerByType.py"              |
|       | ARI_SHORTCUTS_Load                        | ! _-RunPythonScript "X:\\...\\ARI_SHORTCUTS_Load.py"                        |
|       | ARI_SRF_CrvHorizontalPlane                | ! _-RunPythonScript "X:\\...\\ARI_SRF_CrvHorizontalPlane.py"                |
|       | ARI_SRF_CrvVerticalPlane                  | ! _-RunPythonScript "X:\\...\\ARI_SRF_CrvVerticalPlane.py"                  |
|       | ARI_SRF_PlanarPlaneFromCrv                | ! _-RunPythonScript "X:\\...\\ARI_SRF_PlanarPlaneFromCrv.py"                |



#Load Shortcuts

```
import rhinoscriptsyntax as rs
import os

def set_alias(alias, macro):
    # Deletes alias if it exists to ensure a clean update
    if rs.IsAlias(alias):
        rs.DeleteAlias(alias)
    rs.AddAlias(alias, macro)
    print("Set Alias: {} -> {}".format(alias, macro))

# --- CONFIGURATION ---

# 1. Base path for your custom scripts
# Note: We use 'r' before the string to handle backslashes correctly
script_path = r"C:\Users\ritiv\Desktop\(RiR) Developement\Rhino Drafting\Scripts"

# 2. Standard Aliases Dictionary
settings = {
    # Line Commands
    "L": "'_Line",
    "SL": "'_Split",
    "TR": "'_Connect",
    "TT": "'_Trim",
    
    # View Commands
    "H": "'_Hide",
    "HI": "'_Isolate",
    "LO": "'_OneLayerOff",
    "WW": "'_CPlane _World _Top",
    "ZS": "'_Zoom _Selected",
    
    # Transform Commands
    "M": "'_Move",
    "EP": "'_PushPull", # Changed from 'E' to 'EP' to avoid conflict with Explode
    "EC": "'_ExtrudeCrv",
    "ES": "'_ExtrudeSrf",
    "E": "'_Explode",
    "ESrf": "'_DupBorder _SelLast _PlanarSrf _SelPrev _Delete _SelLast",
    "P": "'_Planar",
    "PC": "'_ProjectToCPlane _Yes",
    "PS": "'_PlanarSrf _SelLast _MergeAllEdges",
    "J": "'_Join",
    "JJ": "'_MergeAllCoplanarFaces",
    "JJJ": "'_MergeAllEdges",
    
    # Boolean Commands
    "BS": "'_BooleanSplit",
    "BU": "'_BooleanUnion _MergeAllEdges _MergeAllCoplanarFaces",
    "BD": "'_BooleanDifference"
}

# 3. Custom Python Script Names
# These will be registered using the script name as the Alias
custom_scripts = [
    "ARI_BLOCK_SuperSelectBlocks",
    "ARI_CRV_SplitAllIntersections",
    "ARI_GEO_CappedSlice",
    "ARI_GEO_Check",
    "ARI_GEO_CleanUnion",
    "ARI_LAYER_IFCandBeamLayers",
    "ARI_OBJ_ObjMoveToLayerByType",
    "ARI_SHORTCUTS_Load",
    "ARI_SRF_CrvHorizontalPlane",
    "ARI_SRF_CrvVerticalPlane",
    "ARI_SRF_PlanarPlaneFromCrv"
]

# --- EXECUTION ---

print("--- Starting Alias Configuration ---")

# Set Standard Aliases
for alias, macro in settings.items():
    set_alias(alias, macro)

# Set Custom Script Aliases
for script_name in custom_scripts:
    # Construct the full file path
    full_file_path = os.path.join(script_path, script_name + ".py")
    
    # Check if file actually exists to avoid broken aliases
    if os.path.exists(full_file_path):
        # Create the macro string: ! _-RunPythonScript "Path"
        macro = '! _-RunPythonScript "{}"'.format(full_file_path)
        set_alias(script_name, macro)
    else:
        print("WARNING: Could not find script at: {}".format(full_file_path))

print("--- Aliases Loaded Successfully ---")


```
