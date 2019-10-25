---
title: ポイント アンド プリント DLL
description: ポイント アンド プリント DLL
ms.assetid: 7ead940e-8426-4756-890f-f3607dc1f9ca
keywords:
- ポイントアンドプリント WDK、Dll
- Dll WDK ポイントアンドプリント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f90fa9f1653422bd0f445a13f5af6222402148a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842354"
---
# <a name="point-and-print-dlls"></a>ポイント アンド プリント DLL





必要に応じて、その名前を**モジュール**レジストリ値に関連付けることによって、特別なポイントアンドプリント DLL を指定できます。 この DLL は、次の2つの関数をエクスポートする必要があります。

<a href="" id="generatecopyfilepaths"></a>[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-generatecopyfilepaths)  
この関数は、サーバーのスプーラとクライアントのスプーラの両方によって呼び出され、**ディレクトリ**レジストリ値によって指定されたディレクトリパスを変更するために使用できます。 ソースパス (サーバー上) または移行先パス (クライアント上)、またはその両方のいずれかを変更できます。

<a href="" id="spoolercopyfileevent"></a>[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)  
この関数は、サーバーのスプーラとクライアントのスプーラの両方によって呼び出され、特定の接続に関連するプリンタイベントの発生を示すイベントコードを受け取ります。

ポイントアンドプリント DLL では、これらの関数のみをエクスポートする必要はありません。 たとえば、Microsoft の ICM コンポーネントによって使用される Mscms は、一連の ICM API 関数もエクスポートします。

**GenerateCopyFilePaths**と**SpoolerCopyFileEvent**をエクスポートするポイントアンドプリント DLL に加えて、他の dll を指定することもできます。 これを行うには、**モジュール**のレジストリキーではなく、**ファイル**のレジストリキーに DLL ファイル名を割り当てます。 (「[キュー固有のファイルのインストール](installing-queue-specific-files.md)」を参照してください)。

インストールアプリケーションが**Setプリンター Dataex**を呼び出すことによってサーバーのレジストリに dll の名前を設定した後、 **Setプリンター dataex**の後続のすべての呼び出しで、dll の[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-spoolercopyfileevent)関数を呼び出します。COPYFILE\_イベントの指定されたイベントコード\_\_プリンター\_DATAEX に設定されています。

**Files**レジストリキーの下に一覧表示されるファイルとは異なり ([キュー固有のファイルのインストールに関する](installing-queue-specific-files.md)ページを参照)、クライアントがプリンターに接続するときに、ポイントアンドプリント DLL がプリントサーバーからクライアントにコピーされることはありません。 代わりに、プリントサーバーへの接続が確立されると、DLL は既にクライアントに常駐していると見なされます。 その結果、ポイントアンドプリント機能に関連しない追加の目的で DLL を使用できるようになります。

クライアントにポイントアンドプリント DLL をインストールする方法の1つは、[プリンターの INF ファイル](printer-inf-files.md)でその名前を依存ファイルとして指定することです。そのため、[ドライバー固有のファイルのダウンロード](downloading-driver-specific-files.md)中に、ファイルをクライアントのドライバーディレクトリにコピーできます。

 

 




