---
title: 鍵\_AudioEngine\_OEMPeriod
description: 鍵\_AudioEngine\_OEMPeriod
ms.assetid: e0cefdbf-7016-4609-a898-592a40b5d430
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76934a2d8fec0ffb775ffef355a32619966d4ec5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332212"
---
# <a name="pkeyaudioengineoemperiod"></a>鍵\_AudioEngine\_OEMPeriod


Windows オーディオ エンジンの実行に事前に定義した間隔として参照される、*周期性*オーディオ エンジンの。 オーディオ エンジンは、Windows 7 および Windows の以降のバージョンで、既定で 10 ミリ秒の周期性を実行します。 INF ファイルと、新しいレジストリ キーを使用する Windows 7、**鍵\_AudioEngine\_OEMPeriod**、オーディオ デバイス ドライバーの周期性をカスタマイズします。 これは、エンドポイントの設定ごと。

INF ファイルから次の抜粋は、使用する方法を示します、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)のオーディオ デバイス ドライバの周期性をカスタマイズします。

```inf
[Version]
Signature="$CHICAGO$"
Class=MEDIA
Provider=%MSFT%
...
[USBAudio]
Include=ks.inf, wdmaudio.inf, wdma_usb.inf
Needs=KS.Registration, WDMAUDIO.Registration, USBAudio.CopyList, USBAudioOEM.AddReg

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,"GLOBAL",USBAudio.Interface
AddInterface=%KSCATEGORY_RENDER%,"GLOBAL",USBAudio.Interface

[USBAudio.Interface]
AddReg=USBAudio.Interface.AddReg, OEMSettingsOverride.AddReg
...
;;
;; All EP\\0 entries in the same grouping
;;
;; Set default periodicity to 8ms
;;
;; 0x013880 == 80000 (HNSTIME) == 8ms
;;
[OEMSettingsOverride.AddReg]
HKR,"EP\\0", %PKEY_AudioEndpoint_Association%,,%KSNODETYPE_ANY%
HKR,"EP\\0", %PKEY_AudioEngine_OEMPeriod%, %REG_BINARY%, 41,00,63,00,08,00,00,00,80,38,01,00,00,00,00,00

[Strings]
PKEY_AudioEndpoint_Association = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioEngine_OEMPeriod = "{E4870E26-3CC5-4CD2-BA46-CA0A9A70ED04},6"
REG_BINARY          = "0x00000001"
```

周期性は VT として指定\_BLOB。 周期性の有効な範囲は 50000 90000 (5 9ms) でも 10000 HNSTIME 単位境界 (たとえば、50000、60000、70000、80000 または 90000) にします。

INF ファイル、次のレジストリから前述の抜粋で\_カスタマイズのバイナリ データが提供されます。

8 ミリ秒の周期性は、80000 として HNSTIME 単位で表されます。 16 進数表記では、この値は 0x013880 として表されます。 この 16 進数の値は、一度に (大きさ) の 4 ビットを記述するが、最下位ビットで最初に、結果は 80,38,01。 これは、REG として提供されている値\_BINARY データ型。

周期性は、VT として指定\_BLOB データ型。 これは、65 の 10 進数の値によって表されます。 16 進形式で 65 は 41 値によって表され、前の INF ファイルの抜粋の表示、REG\_41 の最初の値でバイナリ データのシーケンス。

 

 





