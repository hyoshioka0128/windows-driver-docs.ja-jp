---
title: UPnP デバイス用のコンテナー ID
description: UPnP デバイス用のコンテナー ID
ms.assetid: 29d2ed0e-e746-4f0a-88f3-bd07d5750485
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab9e222fe45049ba9f563266192954f8c9b27669
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363451"
---
# <a name="container-ids-for-upnp-devices"></a>UPnP デバイス用のコンテナー ID


Windows 7 以降、PnP 拡張機能 (PNP-X) とユニバーサル PnP (UPnP) をサポートするデバイス ID を指定できます、コンテナーを含めることによって、 **X_containerId**デバイスの説明ドキュメント内の XML 要素。 詳細については、UPnP および UPnP デバイスの説明ドキュメントを参照してください、 [UPnP デバイスのアーキテクチャの仕様。](https://go.microsoft.com/fwlink/p/?linkid=142402)

**X_containerId** XML 要素が次のように宣言されています。

```cpp
<df:X_containerId xmlns:df="">
  xs:string
</df:X_containerId>
```

**X_containerId** XML 要素の型が、値はグローバルに一意の識別子、文字列 (*GUID*)。 この文字列として書式設定 *{xxxxxxxx xxxx-xxxx-。}* します。

例を次に、 **X_containerId** XML 要素。

```cpp
<df:X_containerId xmlns:df="">
  {101392d0-5e91-11dd-ad8b-0800200c9a66}
</df:X_containerId>
```

**X_containerId** XML 要素が必要ですが、&lt;デバイス&gt;UPnP デバイスの説明のドキュメントの「します。 次の例では、適切な配置、 **X_containerId**デバイスの説明ドキュメント内の要素。

**注**  これは UPnP デバイスの説明の完全なドキュメントではありません。 UPnP に関する詳細についてを参照してください、 [UPnP デバイスのアーキテクチャの仕様。](https://go.microsoft.com/fwlink/p/?linkid=142402)

 

```cpp
<?xml version="1.0" ?> 
<root 
 xmlns="urn:schemas-upnp-org:device-1-0"
 xmlns:df=
 "http://schemas.microsoft.com/windows/2008/09/devicefoundation">

 <specVersion>
        <major>major version number</major> 
        <minor>minor version number</minor> 
    </specVersion>

    <URLBase>device URL</URLBase> 

    <device>
 <!-- Place device metadata here. See UPnP spec for details.-->
        <df:X_containerID>
 <!--- Place the ContainerID GUID here.--->
 {101392d0-5e91-11dd-ad8b-0800200c9a66}
      </ df:X_containerID >

    </device>
</root>
```

UPnP デバイスの説明ドキュメントが含まれていない場合、 **X_containerId** 、プラグ アンド プレイ (PnP) マネージャーである XML 要素には、コンテナー ID、デバイスの一意なデバイス名 (UDN) を通じてが生成されます。

 

 





