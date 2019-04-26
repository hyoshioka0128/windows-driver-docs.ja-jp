---
title: パッケージ対応ドライバーの INF を更新する
description: パッケージ対応ドライバーの INF を更新する
ms.assetid: d0bf489d-d084-40df-b5aa-69cdf679993f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a58709ac71945097fb69619f9225d95bf72d788a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346536"
---
# <a name="updating-your-package-aware-drivers-inf"></a>パッケージ対応ドライバーの INF を更新する


パッケージに対応した、ドライバーを使用したコア ドライバーをバンドルする後、次の手順では、パッケージに対応したドライバーの INF ファイルを更新します。

パッケージに対応したドライバーの INF ファイルでは、中核となる更新されたドライバー パッケージを参照する必要があります。 これには、core モデル GUID とに、コアのドライバー パッケージを識別で説明したよう[書き込みコア ドライバー](writing-core-drivers.md)します。 Core のドライバー パッケージを識別するだけでなくは、INF ファイルに次の 2 つの変更を加える必要があります。

最初に、更新されたバージョンのみが使用できるように、中核となるドライバーの最小許容バージョンを指定します。 最小バージョンを指定すると、コアのドライバー パッケージの互換性のない古いバージョンと共にインストールされているパッケージに対応したドライバーの可能性がなくなります。 最小バージョンを指定するには、次の例に示すように、INF InboxVersionRequired ディレクティブを使用します。

```cpp
[PrinterPackageInstallation.x86]
PackageAware=TRUE
CoreDriverDependencies={D20EA372-DD35-4950-9ED8-A6335AFE79F0}
InboxVersionRequired=<version of the updated core driver>
```

前の例では、適切なドライバーのバージョン情報で斜体のテキストを置き換えます。

次に、使用、 [ **INF CopyINF ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547317)中核となる更新されたドライバー パッケージをドライバー ストアにコピーします。 このディレクティブは、Windows vista のドライバー ストアにコピーをサポートするために更新されました。

次の手順を完了すると、ドライバーをテストする準備があります。 PnP のインストール中に、インストーラーが、新しいパッケージに対応したドライバーを検出し、関連付けられている INF ファイルを読み取る。 CopyINF ディレクティブが強制的に更新されたコアのドライバー パッケージ、ドライバー ストアに読み込まれると、パッケージに対応したドライバーのインストールの残りの部分が続行されます。

 

 




