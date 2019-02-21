---
title: プリンターの INF ファイルのデータ セクション
description: プリンターの INF ファイルのデータ セクション
ms.assetid: d060716c-7c26-41a8-afbc-6fe83829d46a
keywords:
- WDK の INF ファイルを印刷するデータ セクション
- データのセクションでは WDK プリンター
- 前の名前のデータ セクション WDK プリンター
- セクションでは WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94320614a29d8ee17c58969f89205e9454793123
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539612"
---
# <a name="printer-inf-file-data-sections"></a>プリンターの INF ファイルのデータ セクション





既定 Windows 2000 以降のプリンター クラス インストーラー Ntprint.dll は、セクションではデータを格納するための INF ファイルをプリンターにできます。 データのセクションでは、次の形式を使用して指定します。

**DataSection**= *SectionName*

場所*SectionName* INF ファイルのセクション名です。

データ セクションがのセットを指定するために使用されています。[プリンター INF ファイルのエントリ](printer-inf-file-entries.md)は複数のプリンターに共通です。 名前付きのセクションでは、一覧内の一般的なエントリをグループ化して、そのセクションを参照する、 **DataSection**エントリを使用する各プリンターのステートメントは、エントリの一覧が、INF ファイルに 1 回だけ含めることが、します。

Microsoft のプリンター INF ファイル、Ntprint.inf では、次のデータのセクションを定義します。

-   \[PSCRIPT\_データ\]

    値を割り当てます、 **DriverFile**、 **ConfigFile**、および**HelpFile** Microsoft PostScript プリンター ドライバーのエントリ。

-   \[UNIDRV\_データ\]

    値を割り当てます、 **DriverFile**、 **ConfigFile**、および**HelpFile** Microsoft ユニバーサル プリンター ドライバーのエントリ。

-   \[UNIDRV\_BIDI\_データ\]

    値を割り当てます、 **DriverFile**、 **ConfigFile**、 **HelpFile**、および**LanguageMonitor** Microsoft Universal のエントリ双方向のプリンターのプリンター ドライバー。

これらのデータ セクションは、ベンダーから提供された INF ファイル内から参照する必要があります。 例については、次を参照してください。 [Unidrv ミニドライバーをインストールする](installing-a-unidrv-minidriver.md)と[Pscript ミニドライバーをインストールする](installing-a-pscript-minidriver.md)します。

**注**  されている、IHV プリンター INF ファイル、**必要があります**エントリまたは**Include** Ntprint.inf を参照するエントリは、INF と同じであるデータ セクション名を含めることはできませんセクション名 Ntprint.inf 内に存在します。 プリンターのベンダーから提供された INF ファイルのデータ セクションの名前を付け、前に、セクション名が Ntprint.inf 内 (任意の型) のセクション名として存在しないことを必ず %windir%/inf/Ntprint.inf を検索します。

 

### <a href="" id="ddk--previous-names-section-gg"></a>「名前」セクション

Windows 2000 以降のプリンター クラスのインストーラーは、「名前」と呼ばれる特殊なデータ セクションを認識します。 これらのセクションの 1 つは、各 INF ファイルで許可されます。 セクションのエントリは、プリンター名の異なる Windows 2000 および Windows 95/98/me のよりも後でドライバーを識別します。 このような名前の相違点を指定すると、Windows 2000 および以降のサーバーに接続する、Windows 95/98/Me クライアントをサポートするには、ポイント アンド プリントができます。

このセクションでは、各エントリの形式です。

"*Windows 2000 またはそれ以降のプリンター名*「=」*Windows 95/98/Me プリンター名*"

次に、エントリの例を示します。

```cpp
[Previous Names]
"HP Color LaserJet" = "HP Color LaserJet (MS)"
"HP DeskJet 1200C" = "HP DeskJet 1200C (MS)"
"HP DeskJet 310" = "HP DeskJet 310 Printer"
```

 

 




