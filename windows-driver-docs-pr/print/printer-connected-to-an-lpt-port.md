---
title: LPT ポートに接続されているプリンター
description: LPT ポートに接続されているプリンター
ms.assetid: fbc71ae8-9b63-4667-b9d6-fdff9100d70b
keywords:
- LPT 列挙子の WDK プリンター
- パラレル ポート WDK、プリンターの接続
- 並列の列挙子の WDk プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47eedb2de388de7a6f65aa3fff62f631c95a9f18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380023"
---
# <a name="printer-connected-to-an-lpt-port"></a>LPT ポートに接続されているプリンター





LPT 列挙子の例に示します、[バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540704)します。 LPT 列挙子に準拠している LPT ポートのハードウェアから id 情報を取得できる、 *IEEE 1284 拡張機能ポート プロトコルと ISA インターフェイス標準*します。

Windows 2000 またはそれ以降のシステム起動すると、configuration manager は、LPT ポートに接続されている IEEE 1284 と互換性のあるデバイスを列挙するために、LPT 列挙子を呼び出します。 検出されたデバイスごとには、構成マネージャーは、プリンター クラスのインストーラーを呼び出します。 プリンター クラスのインストーラー呼び出し**SetupDi**-プレフィックス[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)から情報を取得する[プリンター INF ファイル](printer-inf-files.md)します。

並列に接続されているプリンターでは、並列の列挙子を作成、 *devnode*に一意*ハードウェア ID*プリンターから受け取る 1284 文字列から生成されました。

1284 文字列の例に示します。

```cpp
"MANUFACTURER:Hewlett-Packard;COMMAND SET:PJL,MLC,PCL,POSTSCRIPT;MODEL:HP Color LaserJet 550;CLASS:PRINTER;COMMENT:HP LaserJet;"
```

この 1284 文字列からは、並列の列挙子は、次のハードウェア ID を生成します。

```cpp
LPTENUM\Hewlett-PackardHP_Co3115
```

ハードウェア ID は、製造元の名前、モデルの名前および巡回冗長検査 (CRC) のコードを列挙子のプレフィックスで構成されます。 ハードウェア ID の最後の 4 桁の数字は、CRC のコードは、製造元とモデルの文字列から生成されます。 文字列内のスペースはアンダー スコアに置き換えられます。

送信するには、デバイスから 1284 ID 文字列を読み取り、 [ **IOCTL\_PAR\_クエリ\_デバイス\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff544076)します。 スプーラが、LPT をリダイレクトすることに注意してください*x*シンボリック リンク (場所*x* LPT 数 1、2、または 3) には、スプーラーの名前付きパイプ、した場合、スプーラが実行されている場合、し parport ことはありませんは確認 Ioctl を送信するにはLPTx します。

下に置くことは、並列に接続されているプラグ アンド プレイ プリンターの devnode **HKLM\\システム\\CurrentControlSet\\Enum\\LPTENUM**であり、フォームの 1 つのハードウェア ID:

```cpp
LPTENUM\Company_NameModelNam1234
```

ドライバー スタックは、次のコード サンプルを次の図に表示されます。

INF コードは正しく「プラグ アンド プレイ」LPTENUM フォームのハードウェア ID を\\*会社\_NameModelNam1234*次の例に示します。 "モデル名 XYZ"デバイスの説明は表示で 2 回、 [ **INF 製造元セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454)します。 最初の行で、ハードウェア ID には、2 番目の行の ID は、ハードウェアの中に、バス列挙子が含まれています。 2 つの行では、プリンターがインストールされているバスの種類に関係なく、ランク 0 のハードウェア ID の一致を保証します。 参照してください[カスタムのプラグ アンド プレイ プリンター ドライバーをインストールする](installing-a-custom-plug-and-play-printer-driver.md)詳細についてはします。

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

![パラレル ポート プリンターのプラグ アンド プレイ](images/pnppar01.png)

共有するプリンターの*デバイス ID* 、他のモデルでは、INF ファイルを次のようなにする必要があります。

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

モデルそれぞれ前の例と同様、 [ **INF 製造元セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454)とほぼ同じ行のペアとして表されます。 特定のモデルのペアの 1 つの行には bus 列挙子が含まれていますもう一方は提供されません。 2 つの行では、プリンターがインストールされているバスの種類に関係なく、ランク 0 のハードウェア ID の一致を保証します。 参照してください[カスタムのプラグ アンド プレイ プリンター ドライバーをインストールする](installing-a-custom-plug-and-play-printer-driver.md)詳細についてはします。

 

 




