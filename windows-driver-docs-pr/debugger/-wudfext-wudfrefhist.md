---
title: wudfext.wudfrefhist
description: Wudfext.wudfrefhist 拡張機能は、UMDF オブジェクトの参照カウントの履歴を表示します。
ms.assetid: 8999f525-c6ed-4341-be2c-b0debef23a4b
keywords:
- デバッグ wudfext.wudfrefhist Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfrefhist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3bc85de50ad2a6837d620e446c69b8a45c7f87b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351586"
---
# <a name="wudfextwudfrefhist"></a>!wudfext.wudfrefhist


**! Wudfext.wudfrefhist**拡張機能は、UMDF オブジェクトの参照カウントの履歴を表示します。

```dbgcmd
!wudfext.wudfrefhist ObjectAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ObjectAddress______"></span><span id="_______objectaddress______"></span><span id="_______OBJECTADDRESS______"></span> *ObjectAddress*   
参照カウントの履歴が表示される UMDF オブジェクトのアドレスを指定します。 これは、インターフェイスのないオブジェクト自体のアドレスであることに注意してください。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wudfext.dll

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>コメント
-------

**! Wudfext.wudfrefhist** UMDF 1.11 によってコマンドがサポートされていません。

*ObjectAddress*パラメーターは、(その他の多数の UMDF 拡張機能コマンドで使用される) インターフェイスのアドレスではなく、UMDF オブジェクトのアドレスを指定する必要があります。 UMDF オブジェクトのアドレスを調べるには、 [ **! wudfext.wudfdumpobjects** ](-wudfext-wudfdumpobjects.md)コマンドで、UMDF オブジェクトのアドレスとインターフェイスのアドレスの両方が表示されます。 また、インターフェイスのアドレスがわかっている場合使えるの引数として、 [ **! wudfext.wudfobject** ](-wudfext-wudfobject.md)コマンドで、オブジェクトのアドレスが表示されます (シンボルの後に表示される"[fx]:")。

参照追跡オプションをカウントする場合 (**TrackRefCounts**) が有効になって WDF Verifier で使用できます **! wudfext.wudfrefhist**オブジェクトの各呼び出し履歴をインクリメントまたはデクリメントを表示するには参照カウントします。 呼び出し履歴が調べることでメモリ リークを起こしているかどうかを指定できます、 **AddRef**と**リリース**呼び出しが行われている参照の追加され、解放されません。

このコマンドは、UMDF が「壊れていないデバッガーに場合でも、いつでもでも使用できます。

このコマンドが必要な情報が表示されない場合で、関連するデータがページングされたことを確認してからやり直してください。

使用する例を次に示します、 **! wudfext.wudfrefhist**コマンド。

```dbgcmd
0:007> !wudfext.umdevstacks
...
      UMDriver Image Path: C:\Windows\System32\drivers\UMDF\WUDFOsrUsbFilter.dll
      Object Tracker Address: 0x0000003792ee9fc0
        Object   Tracking ON
        Refcount Tracking ON

0:007> !wudfext.wudfdumpobjects 0x0000003792ee9fc0
...
WdfTypeIoQueue   Object: 0x0000003792f05ce0, Interface: 0x0000003792f05d58

## 0:007> !wudfext.wudfrefhist 0x0000003792f05ce0
-----------------------------------------------------------------------
## 2  (++)
-----------------------------------------------------------------------
WUDFx!UfxObject::TrackRefCounts+0xb2
WUDFx!CWdfIoQueue::AddRef+0x17adc
WUDFx!CWdfIoQueue::CreateAndInitialize+0xeb
WUDFx!CWdfDevice::CreateIoQueue+0x1e7
WUDFOsrUsbFilter!CMyQueue::Initialize+0x48
WUDFOsrUsbFilter!CMyDevice::Configure+0x7d
WUDFOsrUsbFilter!CMyDriver::OnDeviceAdd+0xca
WUDFx!CWdfDriver::OnAddDevice+0x486
WUDFx!CWUDF::AddDevice+0x43
WUDFHost!CWudfDeviceStack::LoadDrivers+0x320
WUDFHost!CLpcNotification::Message+0x1340
WUDFPlatform!WdfLpcPort::ProcessMessage+0x140
WUDFPlatform!WdfLpcCommPort::ProcessMessage+0x92
WUDFPlatform!WdfLpc::RetrieveMessage+0x20c
```

 

 





