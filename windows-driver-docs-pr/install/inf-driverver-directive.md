---
title: INF DriverVer ディレクティブ
description: DriverVer ディレクティブでは、この INF によってインストールされたドライバーのバージョン情報を指定します。
ms.assetid: b8c17839-a027-4fb6-b017-8e9a3fd0d694
keywords:
- INF DriverVer ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DriverVer Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a81f9fea8cb3b1afe8a57b2d2235b10175f7b180
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372351"
---
# <a name="inf-driverver-directive"></a>INF DriverVer ディレクティブ


A **DriverVer**ディレクティブがこの INF によってインストールされたドライバーのバージョン情報を指定します。

```ini
[Version] |
[DDInstall]
 
DriverVer=mm/dd/yyyy,w.x.y.z 
```

## <a name="entries"></a>エントリ


<a href="" id="mm-dd-yyyy"></a>*年/月/日*  
この値の日付を指定します、"[ドライバー パッケージ](driver-packages.md)"、ドライバー ファイル、および、INF が含まれます。 この日付は、ドライバー パッケージ内のすべてのファイルの最新の日付である必要があります。

日付は、月/日/年の順序で指定する必要があります。 月と日は、2 桁の数字を含める必要があり、年は 4 桁の数字を含める必要があります。 ハイフン (-) は、スラッシュ (/) ではなく日付フィールドの区切り記号として使用できます。

<a href="" id="w-x-y-z"></a>*w.x.y.z*  
この値は、バージョン番号を指定します。

各*w*、 *x*、 *y*、および*z* 0 以上 65535 未満である整数にする必要があります。

Windows XP SP1、Windows Server 2003 と以降のバージョンの Windows では、この値はまた、*使用*ドライバーのランクとデバイスのドライバーを選択する、日付の組み合わせで、セットアップでします。 詳細については、次を参照してください。 [Windows ドライバーを選択する方法](how-setup-selects-drivers.md)します。

次の点は、Windows 2000、および Windows XP には、この値に適用されます。

-   この値はのみ (たとえばデバイス マネージャーで) 表示目的で使用、デバイスのドライバーを選択するのには使用されません。
-   (マウスやキーボード ドライバーなど) などの入力のドライバを必須にするには、この値を考慮する必要があります。 バージョンの値を含めないでください、入力のドライバがプログラムによって更新されない可能性があります。 通常、すべてのバージョン情報を指定する必要があります[ドライバー パッケージ](driver-packages.md)のため、オペレーティング システムが最新のドライバーを特定の条件としてバージョン情報を使用します。

<a name="remarks"></a>コメント
-------

Windows 2000 以降、INF ファイルがある必要があります、 **DriverVer**ディレクティブで、 [ **INF バージョン セクション**](inf-version-section.md)全体の INF のバージョン情報を提供します。 個別[ **INF *DDInstall*セクション**](inf-ddinstall-section.md)も含めることができます**DriverVer**個々 のバージョン情報を提供するためのディレクティブドライバーです。 **DriverVer**ディレクティブ、 *DDInstall*のセクションではより固有であり、グローバルよりも優先**DriverVer**ディレクティブで、**バージョン**セクション。

オペレーティング システムは、ドライバーを検索する場合より最近のあるドライバーを選択します。 **DriverVer**ドライバーの以前の日付を日付。 INF にない場合**DriverVer**ディレクティブまたは、無効な日付の仕様が含まれているオペレーティング システムが 00、構造体、0000 00 の既定の日付を適用します。 Windows 2000 の場合、署名されていないドライバー 0000/00/00 の日付も割り当てます。

<a name="examples"></a>使用例
--------

```ini
[Version]
...
DriverVer=09/28/1999,5.00.2136.1
```

## <a name="see-also"></a>関連項目


[***DDInstall***](inf-ddinstall-section.md)

[**バージョン**](inf-version-section.md)

 

 






