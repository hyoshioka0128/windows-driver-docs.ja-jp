---
title: HD オーディオ ドライバー音量設定のカスタマイズ
description: HD オーディオ トレイをカスタマイズする機能は、既定のオーディオ音量とマイク ブーストのレベルに合わせて特定の PC、インストール パラメーター オーディオのアダプターは、ある程度の柔軟性を Oem に提供します。
ms.assetid: 0C86C869-447E-4A77-A723-5D9A17D95C7C
keywords:
- オーディオの音量の設定
- オーディオ アダプター WDK、ボリュームの設定
- アダプターのドライバー WDK オーディオ、ボリュームの設定
- オーディオの音量の設定をカスタマイズします。
- ポート クラス オーディオ アダプター WDK、ボリュームの設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f5ba4155d7a499646fadbee71b166d7c816f441
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333841"
---
# <a name="customizing-hd-audio-driver-volume-settings"></a>HD オーディオ ドライバー音量設定のカスタマイズ


HD オーディオ トレイをカスタマイズする機能は、既定のオーディオ音量とマイク ブーストのレベルに合わせて特定の PC、インストール パラメーター オーディオのアダプターは、ある程度の柔軟性を Oem に提供します。

**注**  ここで説明したプロセスは、既定の Microsoft HD オーディオ ドライバーを使用している場合にのみ使用できます。

 

既定では、HD オーディオ クラス関数ドライバー、オーディオのボリュームを設定して、ユーザーのエクスペリエンスのマイク ブーストのレベル「すぐに」楽しいことを確認する事前に定義された値。

HD オーディオのクラス関数ドライバー、オーディオ クラス ドライバーとしてを今すぐ参照は、任意の特定の PC 用にカスタマイズすることはできません、さまざまなハード コーディングされた既定値を使用します。 そのため、Oem では、各自の要件を満たすためにこれらの値をオーバーライドすることはできません。 ボリューム レベルは、特に初回使用時に、ユーザーは、オーディオ システムの quietness、ラウドネスに機密性の高いを調整する最も重要な設定の 1 つです。

オーディオ クラス ドライバーはハード コーディングされた既定値を上書きできるように再設計されました。 オーディオ クラス ドライバーのハード コーディングされた値をオーバーライドするためのメカニズムでは、オーディオ クラス ドライバーの受信トレイ INF ファイル (hdaudio.inf) をラップする INF ファイルの書き込みと、このラッパー INF を使用して、目的の値を指定する必要があります。

サンプル HD オーディオ コーデックのトポロジを表示する次の図。 Pin ・ コンプレックスの Id と同様に、個々 のノードの Id があることに注意してください。![pin ・ コンプレックス物理のコネクタを表すことを示すオーディオ コーデックのトポロジをサンプルします。 mic と行の入力ノード、およびスピーカー ノード show 暗証番号 (pin) の複雑な id を出力します。](images/pin-complexid2.png)

Pin ・ コンプレックス (スピーカー、マイク、または行) に関連付けられているデバイスの物理的なコネクタを表します。

ごとのカスタムのレベルを指定するラッパー INF ファイルをカスタム オーディオ ボリューム レベルまたはマイク ブースト レベル、使用を指定するには、複雑な id。 をピン留め レベルは、既定のカーネル クラス ドライバーを返す必要があります (KS) デシベル レベルのストリーミングを表す Dword として表現されます。

HD オーディオ クラス ドライバーが KSPROPERTY の GET 要求を受信すると\_オーディオ\_VOLUMELEVEL、ドライバーの決定が既定のボリューム (またはマイク ブースト) があるかどうかを受信したノードを含むパスのレジストリの値要求。 レジストリの既定値が、デバイスに適用され、KSPROPERTY にも返されます場合は、レジストリの値がある、以前にキャッシュされた値がない、\_オーディオ\_VOLUMELEVEL 応答します。 レジストリの値がない場合、HD オーディオ クラス ドライバー サブデバイス グラフの実装から既定値を取得します。

Windows Vista 以降、既定値としては、

-   エンドポイントのボリュームの既定値からすべてのデバイスの種類の 6 dB マイナス max です。

-   マイク ブーストの既定値は dB 0 です。

次の手順が KSPROPERTY の GET 要求に応答で返される既定値を決定するオーディオ クラス ドライバーによって使用されるアルゴリズムをまとめて\_オーディオ\_VOLUMELEVEL:

1. Pin の複雑なクエリ [ボリューム] ノードを含むパスの終了を決定します。

2. 手順 1 で見つかった pin の複雑なため、ボリュームまたはマイク ブーストの既定値が指定されてかどうかを確認するレジストリのルックアップを実行します。

3. レジストリの値が見つかった場合、ドライバー値を設定しその、最小値をアンプでサポートされる最小値を下回る場合。 それ以外の場合、値は、アンプでサポートされる最大値の上にある場合に、最大値に設定されます。 レジストリで見つかった値が、アンプでサポートされる範囲内にある場合は、値が、GET 要求に対する応答で返されます。 さらに、ドライバーはプログラムの表示またはピン留めする複雑なからキャプチャするときに、この値を持つ関連する HD オーディオ アンプ ウィジェットです。

次のフォルダー ツリーは、既定値を保持するドライバーのインスタンス キーのレイアウトを示します。

&lt;ドライバー キー&gt; DefaultVolumeLevels 暗証番号 (pin) の複雑な (2 桁の 16 進数、"0 x"が付いていない) ボリューム (DWORD KS DB の手順で) 向上 (DWORD KS DB の手順で)

KS DB ステップ実行値は次のように定義されます infinity デシベル (減衰) は-2147483648。

-2147483647 は-32767.99998474 デシベル (減衰)

+ 2147483647 までは +32767.99998474 デシベル (向上)

(1/65536 db) を使用する測定単位の詳細については、次を参照してください。 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309)します。

Wdmudio.inf ファイルを上書きするには、Include およびニーズ ディレクティブ使用からこのコード セグメントで示すように、 *Microsoft 仮想のオーディオ デバイス ドライバー サンプル*として使用できるの一部、 [Windows Driver Kit (WDK) 8.1 サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052).

```inf
;Copyright (c) Microsoft Corporation. All rights reserved.
;
...
[MSVAD_Simple.NT]
Include=ks.inf,wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration
...
```

Include およびニーズ ディレクティブの詳細については、次を参照してください。 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)と[INF ファイルのソース メディア](https://msdn.microsoft.com/library/windows/hardware/ff552302)します。

オーディオ クラス ドライバーの INF ファイルをラップするサンプル INF ラッパーを次に示します。

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

HKR の相対パスが指定されてために使用される特定の INF ファイルのセクションに基づく正確なドライバーのレジストリ パスが決定されます。 HKR の相対パスの詳細については、次を参照してください。 [ **INF AddReg ディレクティブ (Windows ドライバー)**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。 次の 2 つのレジストリ パスは、例、レジストリのパスを異なる可能性が高い。

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Class\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002

- - または -

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Class\\{4d36e96c-e325-11ce-bfc1-08002be10318}\\0002\\DeviceInterfaces\\eAuxIn

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[既定のオーディオの音量の設定](default-audio-volume-settings.md)  
[**KSPROPERTY\_オーディオ\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309)  



