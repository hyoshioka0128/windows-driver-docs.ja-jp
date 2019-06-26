---
title: INF CopyINF ディレクティブ
description: CopyINF ディレクティブは、ターゲット システムにコピーする INF ファイルを指定します。 CopyINF ディレクティブは、Windows XP および Windows の以降のバージョンでサポートされます。
ms.assetid: 289822a8-69c3-43a3-ab07-ee02a7473db8
keywords:
- INF CopyINF ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF CopyINF Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 548d5335bd99c190b10466e2b336af46c9619cd0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378025"
---
# <a name="inf-copyinf-directive"></a>INF CopyINF ディレクティブ


A **CopyINF**ディレクティブにより、ターゲット システムにコピーする INF ファイルを指定します。 **CopyINF**ディレクティブは、Windows XP および以降のバージョンの Windows でサポートされます。

```ini
[DDInstall]
  
CopyINF=filename1.inf[,filename2.inf]...
```

<a name="remarks"></a>コメント
-------

システムのサポート、 **CopyINF**ディレクティブは Microsoft Windows XP 以降のバージョンの Windows で使用できます。

このディレクティブは、多機能デバイスをインストールするときに通常使用されます。 多機能デバイスのインストールでは、複数の INF ファイル (複数のセットアップ クラスに属している複数の関数) を必要とする場合は、関数をインストールするときに、Windows が INF ファイルを見つけることによりこのディレクティブを使用します。 次の規則を使用します。

-   場合は、多機能デバイスによって提供される関数は、親デバイス (IEEE 1284.4 デバイスの場合) などの子として列挙されますが、親デバイスの INF ファイルが必要、 **CopyINF**ディレクティブ、INF をコピーするファイルをデバイスの個々 の関数。

-   各関数の INF ファイルがある必要があります (pci) などの多機能デバイスによって提供されるすべての関数は、1 つ別のピアとして列挙されますが場合、 **CopyINF**ディレクティブ、INF をコピーするファイルのすべてのピア関数。

これらの規則に従うと、Windows は、各関数のインストール ディスクのユーザーに確認しないで関数ごとにドライバーをインストールできます。

次の点を適用する、 **CopyINF**ディレクティブ。

-   Windows Vista では、前に Windows が既定の処理の一環として、指定した INF ファイルをコピー [ **DIF_INSTALLDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice) (を参照してください[ **SetupDiInstallDevice** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)) デバイスが正常にインストールされます。

    Windows では、デバイスのインストール中に検索、システムのディレクトリ パスに指定した INF ファイルをコピーします。

-   INF ファイルで指定されている、 **CopyINF**ディレクティブは、格納している INF ファイルと同じディレクトリ内に存在する必要があります、 **CopyINF**ディレクティブ。
-   マルチ ディスク インストールの各ディスク上のすべての INF ファイルを含める必要があります。

Windows Vista 以降では、次の点にも適用されます、 **CopyINF**ディレクティブ。

-   **CopyINF**ディレクティブにより、完全な[ドライバー パッケージ](driver-packages.md)にコピーされる指定した INF ファイルによって参照される、[ドライバー ストア](driver-store.md)します。 これは、機能は、デバイスが実際にインストールされている場合、元のソース メディアは使用できないため、多機能のドライバー パッケージの展開をサポートするために必要です。 INF ファイルがで指定された、指定した INF ファイルによって既に参照されているドライバー パッケージがドライバー ストアに存在する場合、 **CopyINF**ディレクティブは無視されます。

-   **CopyINF**ディレクティブがドライバー ストアのインポートの代わりにデバイスのインストール中に処理されます。 つまり、呼び出しを[SetupCopyOEMInf](https://go.microsoft.com/fwlink/p/?linkid=194252) Windows Vista および Windows の以降のバージョンがすべて、 **CopyINF**その時点で処理される指定した INF ファイルでディレクティブ。 各再帰的に発生するこの**CopyINF**すべての参照先のドライバー パッケージがドライバー ストアにコピーされるまで、指定した INF ファイルに含まれるディレクティブです。

Windows 10、特定の状況では、バージョン 1511 以降では (たとえば、Windows Update または呼び出しをいくつか実行している[ **DiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice))、Inf でコピー **CopyINF**適用可能なデバイスにもインストールされます。

INF ファイルをコピーする方法の詳細については、次を参照してください。[コピー Inf](copying-inf-files.md)します。

<a name="examples"></a>使用例
--------

```ini
[MyMfDevice.NTx86]
CopyINF = Sound.INF
```

 

 





