---
title: JavaScript デバッガーのスクリプト例
description: このトピックでは、ユーザーおよびカーネルモードの JavaScript コードサンプルについて説明します。たとえば、データフィルター処理プラグアンドプレイデバイスツリーのサンプルです。
ms.assetid: F477430B-10C7-4039-9C5F-25556C306643
ms.date: 02/27/2019
ms.localizationpriority: medium
ms.openlocfilehash: c58f8382cf8b3790a53d06642ee5caa18bf698ec
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166668"
---
# <a name="javascript-debugger-example-scripts"></a>JavaScript デバッガーのスクリプト例

このトピックでは、次のユーザーとカーネルモードの JavaScript コードサンプルについて説明します。

- [プロセスアーキテクチャの決定](#processarchitecture)
- [データのフィルター処理: KD のデバイスツリーのプラグアンドプレイ (カーネルモード)](#filter)
- [マルチメディアに固有のデバイスの拡張 (カーネルモード)](#multimedia)
- [\_デバイス\_オブジェクトへのバス情報の追加 (カーネルモード)](#bus)
- [アプリケーションタイトルの検索 (ユーザーモード)](#title)

## <a name="microsoft-github-repo-example-scripts"></a>Microsoft GitHub リポジトリのサンプルスクリプト

デバッガーチームは、JavaScript のスクリプトと拡張機能の例を含む GitHub リポジトリをホストします。

詳細については、 https://github.com/Microsoft/WinDbg-Samples を参照してください。

Readme ファイルには、使用可能な現在のコード例が記述されています。

## <a name="span-idworking_with_samplesspanspan-idworking_with_samplesspanspan-idworking_with_samplesspanworking-with-samples"></a><span id="Working_with_Samples"></span><span id="working_with_samples"></span><span id="WORKING_WITH_SAMPLES"></span>サンプルの使用

すべてのサンプルをテストするには、一般的なプロセスを使用します。

1. サンプル JavaScript がカーネルモードまたはユーザーモードのデバッグ用であるかどうかを判断します。 次に、適切なダンプファイルを読み込むか、ターゲットシステムへのライブ接続を確立します。

2. メモ帳などのテキストエディターを使用して、という名前のテキストファイルを作成し、HelloWorld ファイル拡張子 ( *HelloWorld*など) を付けて保存します。

```javascript
// WinDbg JavaScript sample
// Says Hello World!

// Code at root will be run with .scriptrun and .scriptload
host.diagnostics.debugLog("***> Hello World! \n");

function sayHi()
{
   //Say Hi 
   host.diagnostics.debugLog("Hi from JavaScript! \n");
}
```

3. [**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load jsprovider.dll
```

4. スクリプトを読み込んで実行するには、 [**scriptrun (スクリプトの実行)** ](-scriptrun--run-script-.md)コマンドを使用します。 *InitializeScript*と*invokeScript*関数名の下にあるコードは、scriptrun コマンドによってルート/top にコードが実行されます。

```dbgcmd
0:000> .scriptrun c:\WinDbg\Scripts\HelloWorld.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\HelloWorld.js'
***> Hello World! 
```

5. スクリプトに一意の名前が付けられた関数が含まれている場合は、dx コマンドを使用して、その関数を実行します。この関数は、デバッガーの状態スクリプトにあります。*ScriptName*。内容.*FunctionName*。

```dbgcmd
0:001> dx Debugger.State.Scripts.HelloWorld.Contents.sayHi()
Hi from JavaScript!
Debugger.State.Scripts.HelloWorld.Contents.sayHi()
```

JavaScript の使用方法の詳細については、 [Javascript デバッガーのスクリプト](javascript-debugger-scripting.md)を参照してください。

## <a name="span-idprocessarchitecturespanspan-idprocessarchitecturespanspan-idprocessarhcitecturespandetermining-process-architecture"></a><span id="Processarchitecture"></span><span id="processarchitecture"></span><span id="PROCESSARHCITECTURE"></span>プロセスアーキテクチャの決定

この JavaScript コードは、"ProcessArchitecture" というプロパティをデバッガーオブジェクトモデルのプロセスオブジェクトに追加して、プロセスが x86 または x64 のどちらであるかを示します。

このスクリプトは、カーネルモードのデバッグをサポートするためのものです。

```JavaScript
"use strict";

class __CheckArchitecture
{
//
// Add a property called 'ProcessArchitecture' on process.
//
    get ProcessArchitecture()
    {
    var guestStates = this.Threads.Any(t=> (!(t.GuestState === undefined) && t.GuestState.Architecture =="x86"));
 
        if(guestStates)
            return "x86";
        else
            return "x64";
    }
};
 
function initializeScript()
{
//
// Extends our notion of a process to place architecture information on it.
//
return [new host.namedModelParent(__CheckArchitecture, "Debugger.Models.Process")];
}
```

カーネルダンプファイルを読み込むか、またはターゲットシステムへのカーネルモード接続を確立します。 次に、JavaScript プロバイダーとサンプルスクリプトを読み込みます。

```dbgcmd
0: kd> !load jsprovider.dll
```

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\processarchitecture.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\processarchitecture.js'
```

[Dx](dx--display-visualizer-variables-.md)コマンドを使用して、現在のプロセスのプロセスアーキテクチャを表示します。

```dbgcmd
2: kd> dx @$curprocess
@$curprocess                 : System [Switch To]
    KernelObject     [Type: _EPROCESS]
    Name             : System
    Id               : 0x4
    Handle           : 0xf0f0f0f0
    Threads         
    Modules         
    Environment     
    Devices         
    Io              
    ProcessArchitecture : x64
```

このサンプルコードでは、常にアーキテクチャを正しく判断できない場合があることに注意してください。 たとえば、32ビットデバッガーを使用しているときにダンプファイルを操作する場合などです。

## <a name="span-idfilterspanspan-idfilterspanspan-idfilterspandata-filtering-plug-and-play-device-tree-in-kd-kernel-mode"></a><span id="Filter"></span><span id="filter"></span><span id="FILTER"></span>データのフィルター処理: KD のデバイスツリーのプラグアンドプレイ (カーネルモード)

このサンプルコードでは、デバイスノードツリーをフィルター処理して、開始された PCI のパスを含むデバイスのみを表示します。

このスクリプトは、カーネルモードのライブデバッグをサポートするためのものです。

! Devnode 0 1 コマンドを使用して、デバイスツリーに関する情報を表示できます。 詳細については、「 [ **! devnode**](-devnode.md)」を参照してください。

```javascript
// PlugAndPlayDeviceTree.js
// An ES6 generator function which recursively filters the device tree looking for PCI devices in the started state.
//
function *filterDevices(deviceNode)
{
    //
    // If the device instance path has "PCI" in it and is started (state == 776), yield it from the generator.
    //
    if (deviceNode.InstancePath.indexOf("PCI") != -1 && deviceNode.State == 776)
    {
        yield deviceNode;
    }
 
    //
    // Recursively invoke the generator for all children of the device node.
    //
    for (var childNode of deviceNode.Children)
    {
        yield* filterDevices(childNode);
    }
}
 
//
// A function which finds the device tree of the first session in the debugger and passes it to our filter function.
//
function filterAllDevices()
{
    return filterDevices(host.namespace.Debugger.Sessions.First().Devices.DeviceTree.First());
}
```

ターゲットシステムへのカーネルモード接続を確立します。

```dbgcmd
0: kd> !load jsprovider.dll
```

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\PlugAndPlayDeviceTree.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\PlugAndPlayDeviceTree.js'
```

FilterAllDevices () 関数を呼び出します。

```dbgcmd
0: kd> dx Debugger.State.Scripts.PlugAndPlayDeviceTree.Contents.filterAllDevices()
Debugger.State.Scripts.PlugAndPlayDeviceTree.Contents.filterAllDevices()                 : [object Generator]
    [0x0]            : PCI\VEN_8086&DEV_D131&SUBSYS_304A103C&REV_11\3&21436425&0&00
    [0x1]            : PCI\VEN_8086&DEV_D138&SUBSYS_304A103C&REV_11\3&21436425&0&18 (pci)
    [0x2]            : PCI\VEN_10DE&DEV_06FD&SUBSYS_062E10DE&REV_A1\4&324c21a&0&0018 (nvlddmkm)
    [0x3]            : PCI\VEN_8086&DEV_3B64&SUBSYS_304A103C&REV_06\3&21436425&0&B0 (HECIx64)
    [0x4]            : PCI\VEN_8086&DEV_3B3C&SUBSYS_304A103C&REV_05\3&21436425&0&D0 (usbehci)
    [0x5]            : PCI\VEN_8086&DEV_3B56&SUBSYS_304A103C&REV_05\3&21436425&0&D8 (HDAudBus)
...
```

上記の各オブジェクトは、自動的に DML をサポートし、他の dx クエリと同様に、を使用してクリックできます。

また、このスクリプトを使用する場合は、LINQ クエリを使用して同様の結果を達成することもできます。

```dbgcmd
0: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.InstancePath.Contains("PCI") && n.State == 776)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.InstancePath.Contains("PCI") && n.State == 776)  
    [0x0]            : PCI\VEN_8086&DEV_D131&SUBSYS_304A103C&REV_11\3&21436425&0&00
    [0x1]            : PCI\VEN_8086&DEV_D138&SUBSYS_304A103C&REV_11\3&21436425&0&18 (pci)
    [0x2]            : PCI\VEN_10DE&DEV_06FD&SUBSYS_062E10DE&REV_A1\4&324c21a&0&0018 (nvlddmkm)
    [0x3]            : PCI\VEN_8086&DEV_3B64&SUBSYS_304A103C&REV_06\3&21436425&0&B0 (HECIx64)
    [0x4]            : PCI\VEN_8086&DEV_3B3C&SUBSYS_304A103C&REV_05\3&21436425&0&D0 (usbehci)
    [0x5]            : PCI\VEN_8086&DEV_3B56&SUBSYS_304A103C&REV_05\3&21436425&0&D8 (HDAudBus)
...
```

## <a name="span-idmultimediaspanspan-idmultimediaspanspan-idmultimediaspanextend-devices-specific-to-multimedia-kernel-mode"></a><span id="Multimedia"></span><span id="multimedia"></span><span id="MULTIMEDIA"></span>マルチメディアに固有のデバイスの拡張 (カーネルモード)

この大規模な JavaScript の例では、マルチメディアに固有の情報を対象としてカーネル \_デバイス\_オブジェクトを拡張し、StreamingDevices をデバッガーセッションに追加します。

このスクリプトは、カーネルモードのデバッグをサポートするためのものです。

StreamingDevices を使用したセッション拡張の選択は、例としてのみ実行されます。 これは、既存のの下にある名前空間の内部でのみ、または \_デバイス\_オブジェクトに対して残されている必要があります。ハードウェア.\* 階層。

```javascript
// StreamingFinder.js
// Extends a kernel _DEVICE_OBJECT for information specific to multimedia 
// and adds StreamingDevices to a debugger session.
//

"use strict";
 
function initializeScript()
{
    // isStreamingDeviceObject: 
    //
    // Returns whether devObj (as a _DEVICE_OBJECT -- not a pointer) looks like it is a device
    // object for a streaming device.
    //
    function isStreamingDeviceObject(devObj)
    {
        try
        {
            var devExt = devObj.DeviceExtension;
            var possibleStreamingExtPtrPtr = host.createPointerObject(devExt.address, "ks.sys", "_KSIDEVICE_HEADER **", devObj);
            var possibleStreamingExt = possibleStreamingExtPtrPtr.dereference().dereference();
            var baseDevice = possibleStreamingExt.BaseDevice;
 
            if (devObj.targetLocation == baseDevice.dereference().targetLocation)
            {
                return true;
            }
        }
        //
        // The above code expects to fail (walking into invalid or paged out memory) often.  A failure to read the memory
        // of the target process will result in an exception.  Catch such exception and indicate that the object does not
        // match the profile of a "streaming device object".
        //
        catch(exc)
        {   
        }
 
        return false;
    }
 
    // findStreamingFDO(pdo):
    //
    // From a physical device object, walks up the device stack and attempts to find a device which
    // looks like a streaming device (and is thus assumed to be the FDO).  pdo is a pointer to 
    // the _DEVICE_OBJECT for the pdo.
    //
    function findStreamingFDO(pdo)
    {
        for (var device of pdo.UpperDevices)
        {
            if (isStreamingDeviceObject(device.dereference()))
            {
                return device;
            }
        }
 
        return null;
    }
 
    // streamingDeviceList:
    //
    // A class which enumerates all streaming devices on the system.
    //
    class streamingDeviceList
    {
        constructor(session)
        {
            this.__session = session;
        }
 
        *[Symbol.iterator]()
        {
            //
            // Get the list of all PDOs from PNP using LINQ:
            //
            var allPDOs = this.__session.Devices.DeviceTree.Flatten(function(dev) { return dev.Children; })
                                                           .Select (function(dev) { return dev.PhysicalDeviceObject; });
 
            //
            // Walk the stack up each PDO to find the functional device which looks like a KS device.  This is
            // a very simple heuristic test: the back pointer to the device in the KS device extension is
            // accurate.  Make sure this is wrapped in a try/catch to avoid invalid memory reads causing
            // us to bail out.
            //
            // Don't even bother checking the PDO.
            //
            for (var pdo of allPDOs)
            {
                var fdo = findStreamingFDO(pdo);
                if (fdo != null)
                {
                    yield fdo;
                }
            }
        }
   }
 
    // streamingDeviceExtension:
    //
    // An object which will extend "session" and include the list of streaming devices.
    //
    class streamingDeviceExtension
    {
        get StreamingDevices()
        {
            return new streamingDeviceList(this);
        }
    };
 
    // createEntryList:
    //
    // An abstraction over the create entry list within a streaming device.
    //    
    class createEntryList
    {
        constructor(ksHeader)
        {
            this.__ksHeader = ksHeader;
        }
 
        *[Symbol.iterator]()
        {
            for (var entry of host.namespace.Debugger.Utility.Collections.FromListEntry(this.__ksHeader.ChildCreateHandlerList, "ks!KSICREATE_ENTRY", "ListEntry"))
            {
                                                            if (!entry.CreateItem.Create.isNull)
                {
                    yield entry;
                }
            }
        }
    }
 
    // streamingInformation:
    //
    // Represents the streaming state of a device.
    //    
    class streamingInformation
    {
        constructor(fdo)
        {
            this.__fdo = fdo;
 
            var devExt = fdo.DeviceExtension;
            var streamingExtPtrPtr = host.createPointerObject(devExt.address, "ks.sys", "_KSIDEVICE_HEADER **", fdo);
            this.__ksHeader = streamingExtPtrPtr.dereference().dereference();
        }
 
        get CreateEntries()
        {
            return new createEntryList(this.__ksHeader);
        }
    }
 
    // createEntryVisualizer:
    //
    // A visualizer for KSICREATE_ENTRY
    //
    class createEntryVisualizer
    {
        toString()
        {
            return this.CreateItem.ObjectClass.toString();
        }
 
        get CreateContext()
        {
            //
            // This is probably not entirely accurate.  The context is not *REQUIRED* to be an IUnknown.
            // More analysis should probably be performed.
            //
            return host.createTypedObject(this.CreateItem.Context.address, "ks.sys", "IUnknown", this);
        }
    }
 
    // deviceExtension:
    //
    // Extends our notion of a device in the device tree to place streaming information on
    // top of it.
    //
    class deviceExtension
    {
        get StreamingState()
        {
            if (isStreamingDeviceObject(this))
            {
                return new streamingInformation(this);
            }
 
            //
            // If we cannot find a streaming FDO, returning undefined will indicate that there is no value
            // to the property.
            //
            return undefined;
        }
    }
 
    return [new host.namedModelParent(streamingDeviceExtension, "Debugger.Models.Session"),
            new host.typeSignatureExtension(deviceExtension, "_DEVICE_OBJECT"),
            new host.typeSignatureRegistration(createEntryVisualizer, "KSICREATE_ENTRY")]
}
```

まず、前述のようにスクリプトプロバイダーを読み込みます。 その後、スクリプトを読み込みます。

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\StreamingFinder.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\StreamingFinder.js'
```

次に、dx コマンドを使用して、スクリプトによって提供される新しい StreamingDevices 機能にアクセスします。

```dbgcmd
0: kd> dx -r3 @$cursession.StreamingDevices.Select(d => d->StreamingState.CreateEntries)
@$cursession.StreamingDevices.Select(d => d->StreamingState.CreateEntries)                
    [0x0]            : [object Object]
        [0x0]            : "e0HDMIOutTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
    [0x1]            : [object Object]
        [0x0]            : "AnalogDigitalCaptureTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x1]            : "AnalogDigitalCapture1Topo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x2]            : "AnalogDigitalCapture2Topo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x3]            : "AnalogDigitalCapture2Wave" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortWaveRT]
        [0x4]            : "HeadphoneTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x5]            : "RearLineOutTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x6]            : "RearLineOutWave" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortWaveRT]
    [0x2]            : [object Object]
        [0x0]            : "GLOBAL" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: IUnknown]
```

## <a name="span-idbusspanspan-idbusspanspan-idbusspanadding-bus-information-to-_device_object-kernel-mode"></a><span id="Bus"></span><span id="bus"></span><span id="BUS"></span>\_デバイス\_オブジェクトへのバス情報の追加 (カーネルモード)


このスクリプトは \_デバイス\_オブジェクトの視覚エフェクトを拡張して、PCI 固有の情報が含まれている BusInformation フィールドを追加します。 このサンプルの方法と namespacing については、まだ説明しています。 これは、JavaScript プロバイダーの機能のサンプルとして考える必要があります。

このスクリプトは、カーネルモードのデバッグをサポートするためのものです。

```javascript
"use strict";

/*************************************************
DeviceExtensionInformation.js:

An example which extends _DEVICE_OBJECT to add bus specific information
to each device object.

NOTE: The means of conditionally adding and the style of namespacing this
are still being discussed.  This currently serves as an example of the capability
of JavaScript extensions.

*************************************************/

function initializeScript()
{
    // __getStackPDO():
    //
    // Returns the physical device object of the device stack whose device object
    // is passed in as 'devObj'.
    //
    function __getStackPDO(devObj)
    {
        var curDevice = devObj;
        var nextDevice = curDevice.DeviceObjectExtension.AttachedTo;
        while (!nextDevice.isNull)
        {
            curDevice = nextDevice;
            nextDevice = curDevice.DeviceObjectExtension.AttachedTo;
        }
        return curDevice;
    }
    
    // pciInformation:
    //
    // Class which abstracts our particular representation of PCI information for a PCI device or bus
    // based on a _PCI_DEVICE structure or a _PCI_BUS structure.
    //
    class pciInformation
    {
        constructor(pciDev)
        {
            this.__pciDev = pciDev;
            this.__pciPDO = __getStackPDO(this.__pciDev);
            this.__isBridge = (this.__pciDev.address != this.__pciPDO.address);
            
            if (this.__isBridge)
            {
                this.__deviceExtension = host.createTypedObject(this.__pciPDO.DeviceExtension.address, "pci.sys", "_PCI_DEVICE", this.__pciPDO);
                this.__busExtension = host.createTypedObject(this.__pciDev.DeviceExtension.address, "pci.sys", "_PCI_BUS", this.__pciPDO);
                
                this.__hasDevice = (this.__deviceExtension.Signature == 0x44696350); /* 'PciD' */
                this.__hasBus = (this.__busExtension.Signature == 0x42696350); /* 'PciB' */
                
                if (!this.__hasDevice && !this.__hasBus)
                {
                    throw new Error("Unrecognized PCI device extension");
                }
            }
            else
            {
                this.__deviceExtension = host.createTypedObject(this.__pciPDO.DeviceExtension.address, "pci.sys", "_PCI_DEVICE", this.__pciPDO);
                
                this.__hasDevice = (this.__deviceExtension.Signature == 0x44696350); /* 'PciD' */
                this.__hasBus = false;
                
                if (!this.__hasDevice)
                {
                    throw new Error("Unrecognized PCI device extension");
                }
            }
        }
        
        toString()
        {
            
            if (this.__hasBus && this.__hasDevice)
            {
                return "Bus: " + this.__busExtension.toString() + " Device: " + this.__deviceExtension.toString();
            }
            else if (this.__hasBus)
            {
                return this.__busExtension.toString();
            }
            else
            {
                return this.__deviceExtension.toString();
            }
        }
        
        get Device()
        {
            if (this.__hasDevice)
            {
                // NatVis supplies the visualization for _PCI_DEVICE
                return this.__deviceExtension;
            }
            
            return undefined;
        }
        
        get Bus()
        {
            if (this.__hasBus)
            {
                // NatVis supplies the visualization for _PCI_BUS
                return this.__busExtension;
            }
            
            return undefined;
        }
    }
    
    // busInformation:
    //
    // Our class which does analysis of what bus a particular device is on and places information about
    // about that bus within the _DEVICE_OBJECT visualization.
    //
    class busInformation
    {
        constructor(devObj)
        {
            this.__devObj = devObj;
        }
        
        get PCI()
        {
            //
            // Check the current device object.  This may be a PCI bridge
            // in which both the FDO and PDO are relevant (one for the bus information
            // and one for the bridge device information).
            //
            var curName = this.__devObj.DriverObject.DriverName.toString();
            if (curName.includes("\\Driver\\pci"))
            {
                return new pciInformation(this.__devObj);
            }
            
            var stackPDO = __getStackPDO(this.__devObj);
            var pdoName = stackPDO.DriverObject.DriverName.toString();
            if (pdoName.includes("\\Driver\\pci"))
            {
                return new pciInformation(stackPDO);
            }
            
            return undefined;
        }
    }
    
    // busInformationExtension:
    //
    // An extension placed on top of _DEVICE_OBJECT in order to provide bus analysis and bus specific
    // information to the device.
    //
    class busInformationExtension
    {
        get BusInformation()
        {
            return new busInformation(this);
        }
    }
    
    return [new host.typeSignatureExtension(busInformationExtension, "_DEVICE_OBJECT")];
}
```

まず、前述のようにスクリプトプロバイダーを読み込みます。 その後、スクリプトを読み込みます。

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\DeviceExtensionInformation.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\DeviceExtensionInformation.js'
```

興味のあるデバイスオブジェクトのアドレスを見つける必要があります。 この例では、audio HDAudBus ドライバーを確認します。

```dbgcmd
0: kd>  !drvobj HDAudBus
Driver object (ffffb60757a4ae60) is for:
 \Driver\HDAudBus
Driver Extension List: (id , addr)
(fffff8050a9eb290 ffffb60758413180)  
Device Object list:
ffffb60758e21810  ffffb60757a67c60
```

スクリプトが読み込まれたら、dx コマンドを使用して、デバイスオブジェクトのバス情報を表示します。

```dbgcmd
0: kd> dx -r1 (*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0))
(*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0))                 : Device for "\Driver\HDAudBus" [Type: _DEVICE_OBJECT]
    [<Raw View>]     [Type: _DEVICE_OBJECT]
    Flags            : 0x2004
    UpperDevices     : None
    LowerDevices     : Immediately below is Device for "\Driver\ACPI" [at 0xffffe000003d9820]
    Driver           : 0xffffe00001ccd060 : Driver "\Driver\HDAudBus" [Type: _DRIVER_OBJECT *]
    BusInformation   : [object Object]

0: kd> dx -r1 (*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation"
(*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation"                 : [object Object]
    PCI              :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class

0: kd> dx -r1 (*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation".@"PCI"
(*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation".@"PCI"                 :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class
    Device           :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class [Type: _PCI_DEVICE]

0: kd> dx -r1 (*((pci!_PCI_DEVICE *)0xffffe000003fe1b0))
(*((pci!_PCI_DEVICE *)0xffffe000003fe1b0))                 :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class [Type: _PCI_DEVICE]
    [<Raw View>]     [Type: _PCI_DEVICE]
    Device           : 0xffffe000003fe060 : Device for "\Driver\pci" [Type: _DEVICE_OBJECT *]
    Requirements    
    Resources       

0: kd> dx -r1 (*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources"
(*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources"                
    BaseAddressRegisters
    Interrupt        : Line Based -- Interrupt Line = 0x10 [Type: _PCI_DEVICE_INTERRUPT_RESOURCE]

0: kd> dx -r1 (*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources".@"BaseAddressRegisters"
(*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources".@"BaseAddressRegisters"                
    [0x0]            : Memory Resource: 0xf0340000 of length 0x4000 [Type: _CM_PARTIAL_RESOURCE_DESCRIPTOR]
```

## <a name="span-idtitlespanspan-idtitlespanspan-idtitlespanfind-an-application-title-user-mode"></a><span id="Title"></span><span id="title"></span><span id="TITLE"></span>アプリケーションタイトルの検索 (ユーザーモード)


この例では、デバッガーの現在のプロセス内のすべてのスレッドを反復処理し、 *\_\_mainCRTStartup*を含むフレームを検索して、CRT の起動時に startupinfo から文字列を返します。 このスクリプトは、JavaScript におけるイテレーション、文字列操作、LINQ クエリの例を示しています。

このスクリプトは、ユーザーモードのデバッグをサポートするためのものです。

```javascript
// TitleFinder.js
// A function which uses just JavaScript concepts to find the title of an application
//
function findTitle()
{
    var curProcess = host.currentProcess;
    for (var thread of curProcess.Threads)
    {
        for (var frame of thread.Stack.Frames)
        {
            if (frame.toString().includes("__mainCRTStartup"))
            {
                var locals = frame.LocalVariables;
 
                //
                // locals.StartupInfo.lpTitle is just an unsigned short *.  We need to actually call an API to
                // read the UTF-16 string in the target address space.  This would be true even if this were
                // a char* or wchar_t*.
                //
                return host.memory.readWideString(locals.StartupInfo.lpTitle);
            }
        }
    }
}
 
//
// A function which uses both JavaScript and integrated LINQ concepts to do the same.
//
function findTitleWithLINQ()
{
    var isMainFrame = function(frame) { return frame.toString().includes("__mainCRTStartup"); };
    var isMainThread = function(thread) { return thread.Stack.Frames.Any(isMainFrame); };
 
    var curProcess = host.currentProcess;
    var mainThread = curProcess.Threads.Where(isMainThread).First();
    var mainFrame = mainThread.Stack.Frames.Where(isMainFrame).First();
 
    var locals = mainFrame.LocalVariables;
 
    //
    // locals.StartupInfo.lpTitle is just an unsigned short *.  We need to actually call an API to
    // read the UTF-16 string in the target address space.  This would be true even if this were
    // a char* or wchar_t*.
    //
    return host.memory.readWideString(locals.StartupInfo.lpTitle);
}
```

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\TitleFinder.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\TitleFinder.js'
```

FindTitle () 関数を呼び出すと notepad.exe が返されます。

```dbgcmd
0:000> dx Debugger.State.Scripts.TitleFinder.Contents.findTitle()
Debugger.State.Scripts.TitleFinder.Contents.findTitle() : C:\Windows\System32\notepad.exe
```

LINQ バージョンを呼び出すと、Findタイトル Withlinq () も notepad.exe を返します。

```dbgcmd
0:000> dx Debugger.State.Scripts.TitleFinder.Contents.findTitleWithLINQ()
Debugger.State.Scripts.titleFinder.Contents.findTitleWithLINQ() : C:\Windows\System32\notepad.exe
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

 

 






