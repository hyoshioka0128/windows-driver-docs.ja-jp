---
title: INF DriverVer ディレクティブ
description: DriverVer ディレクティブは、この INF によってインストールされるドライバーのバージョン情報を指定します。
ms.assetid: b8c17839-a027-4fb6-b017-8e9a3fd0d694
keywords:
- INF DriverVer ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DriverVer Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac05af47a91018e15a7fc5a2dd6a9d3c47513dcc
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223170"
---
# <a name="inf-driverver-directive"></a>INF DriverVer ディレクティブ


**DriverVer**ディレクティブは、この INF によってインストールされるドライバーのバージョン情報を指定します。

```inf
[Version] |
[DDInstall]
 
DriverVer=mm/dd/yyyy,w.x.y.z 
```

## <a name="entries"></a>エントリ


<a href="" id="mm-dd-yyyy"></a>*mm/dd/yyyy*  
この値は、ドライバーファイルと INF を含む "[ドライバーパッケージ](driver-packages.md)" の日付を指定します。 この日付は、ドライバパッケージ内のすべてのファイルの最新の日付である必要があります。

日付は、月/日/年の順序で指定する必要があります。 月と日は2桁にする必要があり、年には4桁の数字を含める必要があります。 ハイフン (-) は、スラッシュ (/) ではなく、日付フィールド区切り記号として使用できます。

<a href="" id="w-x-y-z"></a>*w.x.y.z. x. z*  
この値は、バージョン番号を指定します。

*W*、 *x*、 *y*、および*z*の各は、0以上65535未満の整数である必要があります。

Windows XP SP1、Windows Server 2003、およびそれ以降のバージョンの Windows では、この値は、デバイスのドライバーを選択するために、セットアップによってドライバーのランクと日付と組み合わせて*使用さ*れます。 詳細については、「 [Windows がドライバーを選択する方法](how-setup-selects-drivers.md)」を参照してください。

Windows 2000 および Windows XP のこの値には、次の点が適用されます。

-   この値は、表示目的でのみ使用されます (たとえば、デバイスマネージャー)。デバイスのドライバーの選択には使用されません。
-   入力ドライバー (マウスやキーボードのドライバーなど) には、この値が必要であると考える必要があります。 バージョンの値を含めない場合、入力ドライバーはプログラムによって更新されない可能性があります。 通常は、すべての[ドライバーパッケージ](driver-packages.md)のバージョン情報を指定する必要があります。これは、オペレーティングシステムが最新のドライバーを決定するための基準としてバージョン情報を使用するためです。

<a name="remarks"></a>解説
-------

Windows 2000 以降では、inf ファイルの inf[**バージョンセクション**](inf-version-section.md)に**DriverVer**ディレクティブが含まれている必要があります。これにより、inf 全体のバージョン情報が提供されます。 個々の[**INF *ddinstall*セクション**](inf-ddinstall-section.md)には、個々のドライバーのバージョン情報を提供する**DriverVer**ディレクティブを含めることもできます。 *Ddinstall*セクションの**DriverVer**ディレクティブはより具体的で、 **Version**セクションの global **DriverVer**ディレクティブよりも優先されます。

オペレーティングシステムは、ドライバーを検索するときに、以前の日付のドライバーよりも新しい**DriverVer**の日付を持つドライバーを選択します。 INF に**DriverVer**ディレクティブがない場合、または無効な日付の指定が含まれている場合は、オペレーティングシステムによって既定の日付00/00/0000 が適用されます。 Windows 2000 のみでは、署名されていないドライバーにも00/00/0000 の日付が割り当てられます。

<a name="examples"></a>例
--------

```inf
[Version]
...
DriverVer=09/28/1999,5.00.2136.1
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**バージョン**](inf-version-section.md)

 

 






