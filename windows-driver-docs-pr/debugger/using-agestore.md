---
title: AgeStore を使用します。
description: AgeStore を使用します。
ms.assetid: 188eac5c-e84c-45a4-a4ea-1c9bfaa93cca
keywords:
- AgeStore を使用して
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa9da713879906cf40472fc5350e9c98ef2f840a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549790"
---
# <a name="using-agestore"></a>AgeStore を使用します。


AgeStore は、ディレクトリまたはその最後アクセス日に基づいて、ディレクトリ ツリー内のファイルを削除するツールです。 その主な用途は、ディスク領域を節約するために、シンボル サーバーや、ソース サーバーで使用されるダウン ストリームのストアから古いファイルを削除するためです。 一般的なファイル削除ツールとしても使用できます。

AgeStore が 1 つのディレクトリのすべてのファイルを削除できます (、*ターゲット ディレクトリ*)、またはツリー内のすべてのディレクトリ (、*ターゲット ツリー*)。 -S オプションは、ツリー全体が対象となることを示します。

削除するターゲット ディレクトリまたはターゲット ツリー内でファイルを指定する 3 つの方法はあります。 Agestore-日付 = 月-日-年コマンドの削除された最後のすべてのファイルが指定した日付より前にアクセスします。 Agestore-日 = 指定した数日前の複数の NumberOfDays コマンドは、最後にアクセスされたすべてのファイルを削除します。 Agestore-サイズ SizeRemaining コマンドでは、ターゲット ディレクトリまたはターゲットのツリーのすべてのファイルを削除します残りのファイルの合計サイズが小さいと、以下になるまで、少なくとも、最近アクセスされたファイル、以降の = *SizeRemaining*.

たとえば、次のコマンドは、c: すべてのファイルを削除します\\2008 年 1 月 7 日前に最後にアクセスされた MyDir:。

```console
agestore c:\mydir -date=01-07-2008
```

次のコマンドは、従属する c: ディレクトリ ツリー内のすべてのファイルを削除します\\シンボル\\30 日前に最後にアクセスされた downstreamstore:。

```console
agestore c:\symbols\downstreamstore -days=30 -s
```

次のコマンドに従属する c: ディレクトリ ツリー内のファイルを削除する\\シンボル\\downstreamstore、最長前に、このツリー内のすべてのファイルの合計サイズまでそれらにアクセスで始まるバイトの数が 50,000 以下です。

```console
agestore c:\symbols\downstreamstore -size=50000 -s
```

-L オプションは、AgeStore を削除しても、このオプションはすべてのファイルを一覧表示するだけですが、ファイルを削除しないとします。 追加-l オプションを使用して目的のコマンドを実行する必要があります、AgeStore コマンドを使用する前にそれらのファイルだけを削除することを確認する予定がある、削除します。

完全なコマンドラインの構文を参照してください。 [ **AgeStore コマンド ライン オプション**](agestore-command-line-options.md)します。

### <a name="span-idrunningagestoreonwindowsvistaandlaterspanspan-idrunningagestoreonwindowsvistaandlaterspanrunning-agestore-on-windows-vista-and-later"></a><span id="running_agestore_on_windows_vista_and_later"></span><span id="RUNNING_AGESTORE_ON_WINDOWS_VISTA_AND_LATER"></span>Windows Vista 以降で実行中の AgeStore

AgeStore にアクセスしていた最後の時刻に基づいたファイルが削除されるため、ファイル システムは、最終アクセス時刻 (LAT) のデータを格納する場合にのみ正常に実行できます。 NTFS ファイル システムでは、LAT データ ストレージできますか、有効または無効にします。 無効の場合、AgeStore は実行されませんが、代わりに、次のエラー メッセージが表示されます。

```console
Last-Access-Time support is disabled on this computer.
Please read the documentation for more details.
```

Windows Vista および Windows の以降のバージョンでは、LAT データ ストレージが既定で無効になっている、最初にこのデータを有効にしない限りしたがって AgeStore は実行されません。

Windows Vista および以降のバージョンの Windows では、LAT データの収集を有効にするのに FSUtil (Fsutil.exe) ツールを使用することができます。 コマンド プロンプト ウィンドウで、次のコマンドを発行します。

```console
fsutil behavior set disablelastaccess 0 
```

次のコマンドを使用して、LAT データの収集を無効にします。

```console
fsutil behavior set disablelastaccess 1 
```

これらの変更は、次の Windows の再起動後も反映されます。

(ただし、日付のみと、時間が格納されている場合)、FAT32 ファイル システムは常に LAT 情報を格納します。 そのため、AgeStore は FAT32 ファイル システムで動作します。 ただし、NTFS LAT を無効にする AgeStore は実行されていないため、ファイル システムが FAT32 の場合でも NTFS LAT を有効する必要があります。

 

 





