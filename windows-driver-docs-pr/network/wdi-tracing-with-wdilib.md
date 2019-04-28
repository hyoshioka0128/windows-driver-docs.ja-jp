---
title: WDILib による WDI トレース
description: WDILib コンポーネントは現在、WPP を使用してトレースをサポートします。 トレース プロバイダーの GUID では、21ba7b61-05f8-41f1-9048-c09493dcfe38 です。 収集して、トレースの表示は、次の手順を使用できます。
ms.assetid: 2F4FFF67-F88A-4CB0-9980-E3710D4F04EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c467aa82abe582f3a25ef49c38211a12919aa4cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362314"
---
# <a name="wdi-tracing-with-wdilib"></a>WDILib による WDI トレース


WDILib コンポーネントは現在、WPP を使用してトレースをサポートします。 トレース プロバイダーの GUID では、{21ba7b61-05f8-41f1-9048-c09493dcfe38} です。 収集して、トレースの表示は、次の手順を使用できます。

## <a name="start-tracing"></a>トレースを開始


トレースを収集するには、管理者コマンド プロンプトから次のコマンドラインを実行します。

```PowerShell
netsh trace start wireless_dbg provider={21ba7b61-05f8-41f1-9048-c09493dcfe38} level=0xff keywords=0xff
```

Netsh トレースのコマンドラインを含むバッチの cmd ファイルを作成することができます。 これにより、必要な場合は、IHV WPP イベントを含めるコマンドを展開できます。

```PowerShell
@echo off
Setlocal
Rem
Rem Example trace script enabling both WDI and IHV WPP events
Rem

Rem
Rem replace IHV_WPP_GUID with your IHV driver GUID and desired trace flags
Rem
Set IHV_WPP_GUID={0160d072-248f-11e2-be71-082e5f28d97c} 0xff 
Set WDI_WPP_GUID={21ba7b61-05f8-41f1-9048-c09493dcfe38} level=0xff keywords=0xff

Rem
Rem Start the trace
Rem 
netsh trace start wireless_dbg provider=%WDI_WPP_GUID% provider=%IHV_WPP_GUID% globallevel=0xff
```

使用することができます ' ワイヤレス\_dbg' オペレーティング システム側のトレースの残りの部分を有効にします。 その他の便利なオプションに 'capture = yes' パケット トレースを有効にして' 永続的な = [はい] のトレースを保持する停止されるまで再起動後に有効になっています。 つまりを再起動後にトレースを有効にする必要はありません。

代わりに、トレース プロバイダーの GUID は、IHV コンポーネントのトレースを収集するために使用されるトレース コマンドに組み込むことができます。

## <a name="stop-tracing"></a>トレースを停止します。


再現コードを取得すると、トレースを停止し、トレースは、次のコマンドを使用して保存します。

```PowerShell
netsh trace stop
```

%Temp% に、トレースが保存されます\\NetTraces\\NetTrace.etl します。

## <a name="convert-wpp-traces-to-text"></a>WPP トレースをテキストに変換します。


トレースは、テキスト変換ツール、WPP でテキストに変換されます。 1 つのオプションでは、Netsh を使用します。

```PowerShell
netsh trace convert NetTrace.etl tmfpath=C:\TMF
```

この例では、c: で\\TMF には (、wdiwifi から生成されます TMFs が含まれています。PDB tracepdb.exe を実行して)。 TMFs が生成されない場合、変換されたトレースは正しく表示されないします。

## <a name="analyze-traces"></a>トレースを分析します。


変換されたテキスト ファイル (NetTrace.txt) は、任意のテキスト ビューアーを使用して表示できます。 使用して、ビューアーにフィルターを追加する機能がある場合は、'\[エラー\]'、'\[Wdi'、および '\[MSG' 興味深い行までトレースのスコープ フィルターが役立つ場合があります。

## <a name="tracing-on-phones"></a>携帯電話のトレース


を電話でトレースするには、トレースするトレース プロバイダーを含む wdiguids.txt として、次のテキストを保存します。

```Text
0C5A3172-2248-44FD-B9A6-8389CB1DC56A        wlansvc
D905AC1D-65E7-4242-99EA-FE66A8355DF8        WlanAPI
abe47285-c002-46d1-95e4-c4aec3c78f50        WFD WPS Provider
9CC9BEB7-9D24-47C7-8F9D-CCC9DCAC29EB        WFD WPS Provider
7D7180B3-A452-4FFF-8D1F-7B32B248AB70        DAF WFD Provider
19e464a4-7408-49bd-b960-53446ae47820        DAS
e176aa66-5cc8-4321-9624-f9c1d2b7bf06        UPnP
71975d00-46bb-4236-bd4f-41a8c72fadfc        DAF UPnP Provider
2B175479-BBE4-4262-AA71-19AFB22A46F5        UPnP
4D946A46-275B-4C9D-B835-0B2160559256        WPS
C100BECE-D33A-4A4B-BF23-BBEF4663D017        WCN
20644520-D1C2-4024-B6F6-311F99AA51ED        MSMSEC
ED092A80-0125-4403-92AC-4C06632420F8        MSMSEC
253F4CD1-9475-4642-88E0-6790D7A86CDE        MSMSEC
7076BF7A-DB99-4A63-8AFE-0BB2AB92997A        1X
5F31090B-D990-4E91-B16D-46121D0255AA        EAPHOST
D905AC1C-65E7-4242-99EA-FE66A8355DF8        NWifi
e49b27dd-b2f0-4571-8c6a-3271a3a3a6b9        VNE wlanvmp
11111111-0000-0000-0000-000000000000        VNE UserMode
c02edc8d-d627-46c9-abd9-c8b78f88c223        VWifiBus
914598a6-28f0-42ac-bf3d-a29c6047a739        VWifiFlt
ad8fe36a-0581-4571-a143-5a3f93e30160        Bluewire devicepairing.dll
14E44EEB-E037-45a5-9CA6-472258724563        Bluewire devicepairingfolder.dll
05516000-0670-11e0-8e5c-f4ce462d9187        ProximityCommon.dll ProximityService.dll
05516002-0670-11e0-8e5c-f4ce462d9187        ProximityUxHost
3475aabe-44ba-49eb-bfd8-de32e88b4f35        Windows.Networking.NearFieldProximity.dll 
8C3E3B78-4E27-48ea-B52C-7BCDC9CC2DA9        WMP 
C9C074D2-FF9B-410F-8AC6-81C7B8E60D0F        MediaEngineCtrlGuid
3496b396-5c43-45e7-b38e-d509b79ae721        WFDPAL
c7491fe4-66f4-4421-9954-b55f03db3186        WiFiDisplay
F9A92EFE-77C3-4D19-8B00-1EE9E7CBE8C1        UX
802ec45b-1e99-4b83-9920-87c98277ba9d        Miradisp
f860141e-94e0-418e-a8a6-2321623c3018        Vlib
0160d072-248f-11e2-be71-082e5f28d97c        WIFI Driver
07C9AAA5-FF6B-44CF-A417-C3BE5A719C0B        WIFI Driver
21ba7b61-05f8-41f1-9048-c09493dcfe38        WDI Driver
D710D46C-235D-4798-AC20-9F83E1DCD557        EapMethod Ttls
E21E2366-917F-4CCC-BFE4-0FD23CB31209        TTLS WPP
7076bf7a-db99-4a63-8afe-0bb2ab92997a        OneX WPP
3A9B0DE9-2A69-413E-9074-444C0E3A81D9        EAP SIM WPP
5F31090B-D990-4E91-B16D-46121D0255AA        Eaphost WPP
6EB8DB94-FE96-443F-A366-5FE0CEE7FB1C        Eaphost
E5C16D49-2464-4382-BB20-97A4B5465DB9        WifiNetworkmanager
5CA18737-22AC-4050-85BC-B8DBB9F7D986        WifiNetworkmanager wpp
CC3DF8E3-4111-48d0-9B21-7631021F7CA6        Dhcpv4 Client
07a29c3d-26a4-41e2-856a-095b3eb8b6ef        Dhcpv6 Client
```

TShell を使用して、デバイスへの接続、ファイルをコピーおよびトレースを開始します。

```PowerShell
open-device 127.0.0.1
cmdd "mkdir \data\test\wlan"
putd wdiguids.txt \data\test\wlan
cmdd tracelog.exe '-start wdiwpp -f \data\test\wlan\wdiwpp.etl -cir 256 -rt -ls -ft 1'
cmdd tracelog.exe '-enable wdiwpp -guid \data\test\wlan\wdiguids.txt -level 0x7fffffff -flag 0x7fffffff'
```

シナリオを実行します。 トレースを停止して、ログを収集に再接続 TShell (必要な) 場合、次のコマンドを実行します。

```PowerShell
cmdd tracelog.exe '-flush wdiwpp'
cmdd tracelog.exe '-stop wdiwpp'
getd \data\test\wlan\wdiwpp.etl
cmdd 'tracelog -flush WiFiDriver -f C:\data\systemdata\etw\wifidriver.etl'
getd 'C:\data\systemdata\etw\wifidriver.etl'
cmdd 'tracelog -flush WiFiSession'
getd 'C:\Data\SystemData\ETW\WiFi.etl.001'
getd 'C:\Data\SystemData\ETW\WiFi.etl.002'
getd 'C:\Data\SystemData\ETW\WiFi.etl.003'
```
