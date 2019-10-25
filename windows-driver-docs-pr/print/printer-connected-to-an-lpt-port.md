---
title: LPT ポートに接続されているプリンター
description: LPT ポートに接続されているプリンター
ms.assetid: fbc71ae8-9b63-4667-b9d6-fdff9100d70b
keywords:
- LPT 列挙子 WDK プリンター
- パラレルポート WDK、プリンター接続
- 並列列挙子 WDk プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e749520ed0942c0f1538f2b9ffb8216db8b55dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840439"
---
# <a name="printer-connected-to-an-lpt-port"></a>LPT ポートに接続されているプリンター





LPT 列挙子は、[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)の一例です。 LPT 列挙子は、 *IEEE 1284 拡張機能ポートプロトコルと ISA インターフェイス標準*に準拠した lpt ポートハードウェアから識別情報を取得できます。

Windows 2000 以降のシステムが起動すると、configuration manager は LPT 列挙子を呼び出して、LPT ポートに接続されている IEEE 1284 互換デバイスを列挙します。 検出された各デバイスについて、configuration manager はプリンタクラスのインストーラーを呼び出します。 Printer クラスインストーラーは、[プリンターの INF ファイル](printer-inf-files.md)から情報を取得する**setupdi**プレフィックス付き[デバイスインストール機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))を呼び出します。

パラレル接続プリンターの場合、並列列挙子は、プリンターから受信する1284文字列から生成された一意の*ハードウェア ID*を持つ*devnode*を作成します。

1284文字列の例を次に示します。

```cpp
"MANUFACTURER:Hewlett-Packard;COMMAND SET:PJL,MLC,PCL,POSTSCRIPT;MODEL:HP Color LaserJet 550;CLASS:PRINTER;COMMENT:HP LaserJet;"
```

この1284文字列から、並列列挙子は次のハードウェア ID を生成します。

```cpp
LPTENUM\Hewlett-PackardHP_Co3115
```

ハードウェア ID は列挙子プレフィックスで構成され、その後に製造元名、モデル名、および巡回冗長検査 (CRC) コードが続きます。 ハードウェア ID の最後の4桁である CRC コードは、製造元とモデルの文字列から生成されます。 文字列内のスペースはアンダースコアに置き換えられます。

デバイスから 1284 ID 文字列を読み取るには、 [**IOCTL\_PAR\_クエリ\_デバイス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id)を送信します。 スプーラは、LPT*x*シンボリックリンク ( *x*が lpt 番号1、2、または 3) をスプーラの名前付きパイプにリダイレクトすることに注意してください。これは、スプーラが実行されている場合、parport は LPTx に送信された ioctl を認識しないことを意味します。

パラレルに接続されたプラグアンドプレイプリンタの devnode は、 **HKLM\\SYSTEM\\CurrentControlSet\\Enum\\lp**に配置され、次の形式のハードウェア ID が1つあります。

```cpp
LPTENUM\Company_NameModelNam1234
```

次のコードサンプルに続く図に、ドライバースタックが表示されます。

次の例に示すように、 *LpNameModelNam1234 um\\Company\_* という形式のハードウェア ID を適切に "プラグアンドプレイ" する INF コードを次に示します。 "モデル名 XYZ" デバイスの説明は、[ [**INF 製造元] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)に2回表示されます。 最初の行のハードウェア ID には bus 列挙子が含まれていますが、2行目のハードウェア ID には含まれていません。 2つの行は、プリンターがインストールされているバスの種類に関係なく、ランク0のハードウェア ID が一致することを保証します。 詳細については[、「カスタムプラグアンドプレイプリンタドライバのインストール](installing-a-custom-plug-and-play-printer-driver.md)」を参照してください。

```cpp
[Manufacturer]
%Company_Name%=Company_Name

; Section name for all drivers for Company_Name
[Company_Name]
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234 ; plus any compatible IDs
"Model Name XYZ" = Install_Section_XYZ, Company_NameModelNam1234 ; plus any compatible IDs

; The install section for the XYZ model
[Install_Section_XYZ]

[Strings]
Company_Name="Company Name"
```

![パラレルポートプリンターのプラグアンドプレイ](images/pnppar01.png)

*デバイス ID*を他のモデルと共有するプリンターの場合、INF ファイルは次のようになります。

```cpp
[Manufacturer]
%Company_Name%=Company_Name

; The section for all drivers for Company_Name
[Company_Name]
"Model Name XYA" = Install_Section_XYA, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs
"Model Name XYA" = Install_Section_XYA, Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs
"Model Name XYB" = Install_Section_XYB, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234; plus any other compatible IDs
"Model Name XYB" = Install_Section_XYB, Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs

; The install sections
[Install_Section_XYA]

[Install_Section_XYB]

[ControlFlags]
InteractiveInstall = LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234

[Strings]
Company_Name = "Company Name"
```

前の例と同様に、[ [**INF 製造元] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)の各モデルは、ほぼ同一の行のペアによって表されます。 特定のモデルでは、ペアの1つの行に bus 列挙子が含まれます。もう1つはありません。 2つの行は、プリンターがインストールされているバスの種類に関係なく、ランク0のハードウェア ID が一致することを保証します。 詳細については[、「カスタムプラグアンドプレイプリンタドライバのインストール](installing-a-custom-plug-and-play-printer-driver.md)」を参照してください。

 

 




