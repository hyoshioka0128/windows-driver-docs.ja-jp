---
title: INF CopyINF ディレクティブ
description: CopyINF ディレクティブを使用すると、指定した INF ファイルがターゲットシステムにコピーされます。 CopyINF ディレクティブは、windows XP 以降のバージョンの Windows でサポートされています。
ms.assetid: 289822a8-69c3-43a3-ab07-ee02a7473db8
keywords:
- INF CopyINF ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF CopyINF Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c14e2387ae368d5d5ae74154b4676d46e318669
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223264"
---
# <a name="inf-copyinf-directive"></a>INF CopyINF ディレクティブ


**Copyinf**ディレクティブを使用すると、指定した INF ファイルがターゲットシステムにコピーされます。 **Copyinf**ディレクティブは、windows XP 以降のバージョンの windows でサポートされています。

```inf
[DDInstall]
  
CopyINF=filename1.inf[,filename2.inf]...
```

<a name="remarks"></a>解説
-------

**Copyinf**ディレクティブのシステムサポートは、MICROSOFT windows XP 以降のバージョンの windows で使用できます。

通常、このディレクティブは、多機能なデバイスをインストールするときに使用されます。 多機能デバイスのインストールに複数の INF ファイルが必要な場合 (複数のセットアップクラスに属する複数の機能の場合)、このディレクティブを使用すると、機能をインストールするときに Windows によって INF ファイルが確実に検出されます。 次の規則を使用します。

-   多機能デバイスによって提供される関数が、親デバイス (IEEE 1284.4 デバイスなど) の子として列挙される場合、親デバイスの INF ファイルには、デバイスの個々の関数の INF ファイルをコピーするための**copyinf**ディレクティブが必要です。

-   多機能デバイス (PCI カードなど) によって提供されるすべての機能が互いのピアとして列挙されている場合、各関数の INF ファイルには、すべてのピア関数の INF ファイルをコピーするための**Copyinf**ディレクティブが必要です。

これらの規則に従うと、各機能のインストールディスクの入力をユーザーに求めることなく、各機能のドライバーをインストールできます。

**Copyinf**ディレクティブには、次の点が適用されます。

-   Windows Vista より前の Windows では、デバイスが正常にインストールされた後に、指定した INF ファイルが[**DIF_INSTALLDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)の既定の処理の一部としてコピーされます ( [**Setupdiinstalldevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)を参照)。

    Windows は、指定された INF ファイルを、デバイスのインストール中に検索するシステムディレクトリパスにコピーします。

-   **Copyinf**ディレクティブで指定されている inf ファイルは、 **copyinf**ディレクティブを含む inf ファイルと同じディレクトリに存在する必要があります。
-   マルチディスクインストールの各ディスクに、すべての INF ファイルを含める必要があります。

Windows Vista 以降では、 **Copyinf**ディレクティブにも次の点が適用されます。

-   **Copyinf**ディレクティブを使用すると、指定した INF ファイルによって参照される完全な[ドライバーパッケージ](driver-packages.md)が[ドライバーストア](driver-store.md)にコピーされます。 これは、デバイスが実際にインストールされたときに元のソースメディアが使用できない可能性があるため、多機能ドライバーパッケージの展開をサポートするために必要です。 指定した INF ファイルによって参照されているドライバーパッケージがドライバーストアに既に存在する場合、 **copyinf**ディレクティブで指定されている inf ファイルは無視されます。

-   **Copyinf**ディレクティブは、デバイスのインストール時ではなく、ドライバーストアのインポート中に処理されます。 これは、Windows Vista 以降のバージョンの Windows で[Setupcopyoeminf](https://go.microsoft.com/fwlink/p/?linkid=194252)を呼び出すと、指定された INF ファイル内のすべての**copyinf**ディレクティブがその時点で処理されることを意味します。 これは、参照されるすべてのドライバーパッケージがドライバーストアにコピーされるまで、指定した INF ファイルに含まれる各**Copyinf**ディレクティブに対して再帰的に実行されます。

Windows 10 バージョン1511以降では、特定の状況下 (Windows Update を実行している場合や、 [**Diinstalldevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)を呼び出す場合など) では、 **copyinf**でコピーされた inf も適用可能なデバイスにインストールされます。

INF ファイルをコピーする方法の詳細については、「 [inf のコピー](copying-inf-files.md)」を参照してください。

<a name="examples"></a>例
--------

```inf
[MyMfDevice.NTx86]
CopyINF = Sound.INF
```

 

 





