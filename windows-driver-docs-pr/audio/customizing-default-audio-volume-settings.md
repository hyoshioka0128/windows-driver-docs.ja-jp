---
title: HD オーディオ ドライバー音量設定のカスタマイズ
description: インボックス HD オーディオの既定のオーディオボリュームとマイクブーストレベルを特定の PC に合わせてカスタマイズする機能により、Oem はオーディオアダプターのインストールパラメーターを柔軟に使用できるようになります。
ms.assetid: 0C86C869-447E-4A77-A723-5D9A17D95C7C
keywords:
- オーディオボリュームの設定
- オーディオアダプター WDK、ボリューム設定
- アダプタードライバー WDK オーディオ、ボリューム設定
- オーディオボリューム設定のカスタマイズ
- ポートクラスオーディオアダプター WDK、ボリューム設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f951ced9ee5720aa9dd81677e02fa9653b79c5b8
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925619"
---
# <a name="customizing-hd-audio-driver-volume-settings"></a>HD オーディオ ドライバー音量設定のカスタマイズ


インボックス HD オーディオの既定のオーディオボリュームとマイクブーストレベルを特定の PC に合わせてカスタマイズする機能により、Oem はオーディオアダプターのインストールパラメーターを柔軟に使用できるようになります。

**Note**ここで説明するプロセスは、既定の Microsoft HD audio driver が使用されている場合にのみ使用できます。  

 

既定では、HD オーディオクラスの関数ドライバーは、事前に設定された値でオーディオボリュームとマイクブーストレベルを設定して、ユーザーにとって快適に使えるようにします。

HD audio クラス関数ドライバーは、オーディオクラスドライバーとして参照されるようになりましたが、ハードコーディングされたさまざまな既定値を使用して、特定の PC 用にカスタマイズすることはできません。 そのため、Oem は、独自の要件を満たすためにこれらの値を上書きすることはできません。 また、特に初回使用時には、ユーザーがオーディオシステムのラウドネスや quietness に依存しているため、調整する最も重要な設定の1つはボリュームレベルです。

オーディオクラスドライバーは、ハードコーディングされた既定値をオーバーライドできるように再設計されました。 オーディオクラスドライバーのハードコーディングされた値をオーバーライドするメカニズムには、オーディオクラスドライバーの受信トレイ INF ファイル (hdaudio .inf) をラップし、このラッパー INF を使用して目的の値を指定する INF ファイルが記述されます。

次の図は、HD audio コーデックトポロジのサンプルを示しています。 個々のノードの Id と、ピン complexes の Id があることに注意してください。![物理コネクタを表すピン複素を示すサンプルオーディオコーデックトポロジ。 mic およびライン入力ノードと、[スピーカー出力] ノードに [複合 id をピン留めする] が表示されます。](images/pin-complexid2.png)

Pin complexes は、関連付けられているデバイスの物理コネクタ (スピーカー、マイク、回線など) を表します。

カスタムオーディオボリュームレベルまたはマイクブーストレベルを指定するには、ラッパー INF ファイルを使用して、pin の複合 ID ごとにカスタムレベルを指定します。 レベルは、クラスドライバーが返す既定のカーネルストリーミング (KS) のデシベルレベルを表す Dword として表現されます。

HD オーディオクラスドライバーが KSK プロパティ\_audio\_VOLUMELEVEL の GET 要求を受信すると、ドライバーは、要求を受信したノードを含むパスの既定のボリューム (または Mic ブースト) 値がレジストリに存在するかどうかを判断します。 レジストリに値があり、以前にキャッシュされた値がない場合は、レジストリの既定値がデバイスに適用され、KSK PROPERTY\_AUDIO\_VOLUMELEVEL 応答にも返されます。 レジストリに値がない場合、HD オーディオクラスドライバーは、サブデバイスグラフの実装から既定値を取得します。

Windows Vista 以降では、既定値は次のようになります。

-   すべてのデバイスの種類について、エンドポイントボリュームの既定値は最大-6 dB です。

-   マイクブーストの既定値は 0 dB です。

次の手順では、KSK PROPERTY\_audio\_VOLUMELEVEL の GET 要求に応答して返す既定値を決定するために、audio クラスドライバーによって使用されるアルゴリズムの概要を示します。

1. クエリされたボリュームノードを含むパスが終了するピンが複雑であることを確認します。

2. レジストリ検索を実行して、手順 1. で見つかった pin の複合にボリュームまたはマイクブーストの既定値が提供されているかどうかを確認します。

3. レジストリ内で値が見つかった場合、ドライバーはその値を最小値に設定します (これが増幅によってサポートされる最小値を下回った場合)。 それ以外の場合、値は最大値に設定され、増幅された最大値を増幅します。 レジストリで見つかった値がアンプでサポートされている範囲内にある場合は、GET 要求に応答して値が返されます。 さらに、ドライバーは、ピンが複雑になったときにレンダリングするときに、関連付けられている HD オーディオアンプウィジェットをこの値でプログラムします。

次のフォルダーツリーには、既定値を保持するドライバーインスタンスキーのレイアウトが表示されます。

&lt;ドライバーキー&gt; DefaultVolumeLevels Pin Complex (2 桁の16進数、先頭が "0x" ではない) ブースト (ks db ステップの dword)

KS DB のステップ実行値は次のように定義されます。-2147483648 は-無限大デシベル (減衰)

-2147483647 は-32767.99998474 デシベル (減衰)

+ 2147483647 が + 32767.99998474 デシベル (取得)

使用される測定単位 (1/65536 dB) の詳細については、「 [**Ksk property\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)」を参照してください。

Wdmudio .inf ファイルをオーバーライドするには、 [Windows Driver Kit (WDK) 8.1 サンプル](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples)の一部として入手可能な*Microsoft 仮想オーディオデバイスドライバーサンプル*のこのコードセグメントに示されているように、Include および必要なディレクティブを使用します。

```inf
;Copyright (c) Microsoft Corporation. All rights reserved.
;
...
[MSVAD_Simple.NT]
Include=ks.inf,wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration
...
```

Include ディレクティブと必要なディレクティブの詳細については、「 [**Inf DDInstall」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)と「 [Inf ファイルのソースメディア](https://docs.microsoft.com/windows-hardware/drivers/install/source-media-for-inf-files)」を参照してください。

オーディオクラスドライバーの INF ファイルをラップするサンプルの INF ラッパーを次に示します。

```text
;Copyright (c) Microsoft Corporation. All rights reserved.
;
;Module Name:
;    HDAUDVOL.INF
;
;Abstract:
;    Wrapper INF file for installing the Microsoft UAA Function Driver for High
;    Definition Audio with specific INF overrides

[Version]
Signature="$Windows NT$"
Class=MEDIA
ClassGuid={4d36e96c-e325-11ce-bfc1-08002be10318}
Provider=Microsoft
DriverVer=07/28/2012,6.2.9201.0
CatalogFile=hdaudvol.cat

[Manufacturer]
Microsoft = Microsoft,ntamd64,ntarm

[ControlFlags]
ExcludeFromSelect = *

;;====================================================================================
;; Edit the PNP ID (HDAUDIO\FUNC_01...) below to match the codec + subsystem you are ;; configuring.
;;====================================================================================

[Microsoft]
%HdAudModel_DefaultVolume_DeviceDesc% = HdAudModel_DefaultVolume, HDAUDIO\FUNC_01&VEN_10EC&DEV_0889&SUBSYS_00000000&REV_1000

[Microsoft.ntamd64]
%HdAudModel_DefaultVolume_DeviceDesc% = HdAudModel_DefaultVolume, HDAUDIO\FUNC_01&VEN_10EC&DEV_0889&SUBSYS_00000000&REV_1000

[Microsoft.ntarm]
%HdAudModel_DefaultVolume_DeviceDesc% = HdAudModel_DefaultVolume, HDAUDIO\FUNC_01&VEN_10EC&DEV_0889&SUBSYS_00000000&REV_1000

;;===================== HdAudModel_DefaultVolume ==============================

[HdAudModel_DefaultVolume]
Include=hdaudio.inf
Needs=HDAudModel
AddReg=HdAudModel_DefaultVolume.HdAudInit

[HdAudModel_DefaultVolume.HW]
Include=hdaudio.inf
Needs=HdAudModel.HW

[HdAudModel_DefaultVolume.Services]
Include=hdaudio.inf
Needs=HdAudModel.Services

[HdAudModel_DefaultVolume.Interfaces]
Include=hdaudio.inf
Needs=HdAudModel.Interfaces

[HdAudModel_DefaultVolume.HdAudInit]
;;====================================================================================
;; Units are in KS dB so 1dB == 65536 (0x00010000)
;; ======================================================================================
HKR,DefaultVolumeLevels\18,Volume,1,00,00,FE,FF ; Set to 0xFFFE0000 to set to -2dB
HKR,DefaultVolumeLevels\18,Boost,1,00,00,0A,00 ; Set to 0x000A0000 to set to 10dB

[Strings]
HdAudModel_DefaultVolume_DeviceDesc = "High Definition Audio Device"
```

HKR の相対パスが指定されているため、正確なドライバーのレジストリパスは、使用される特定の INF ファイルのセクションに基づいて決定されます。 HKR の相対パスの詳細については、「 [**INF AddReg ディレクティブ (Windows ドライバー)**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」を参照してください。 次の2つのレジストリパスは例ですが、レジストリパスが異なる可能性があります。

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\クラス\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002

- - または -

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Class\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002\\deviceinterfaces\\eAuxIn

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[既定のオーディオ音量の設定](default-audio-volume-settings.md)  
[**KSK プロパティ\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)  



