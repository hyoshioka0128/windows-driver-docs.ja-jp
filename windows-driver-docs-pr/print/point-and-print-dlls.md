---
title: ポイント アンド プリント DLL
description: ポイント アンド プリント DLL
ms.assetid: 7ead940e-8426-4756-890f-f3607dc1f9ca
keywords:
- ポイント アンド プリントの WDK、Dll
- Dll の WDK ポイントと印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5e9da73dc21c9620b37b4247a38821d4b2879c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383536"
---
# <a name="point-and-print-dlls"></a>ポイント アンド プリント DLL





必要に応じて、その名前を関連付けることによって、特殊なポイントと印刷の DLL を指定、**モジュール**レジストリ値。 この DLL は、次の 2 つの関数をエクスポートする必要があります。

<a href="" id="generatecopyfilepaths"></a>[**GenerateCopyFilePaths**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-generatecopyfilepaths)  
指定されたディレクトリ パスを変更するのには、サーバーのスプーラとクライアントのスプーラーの両方で呼び出されると、この関数を使用できます、**ディレクトリ**レジストリ値。 (サーバー) 上のソース パスまたは (クライアント) で移行先パスの両方またはいずれかを変更できます。

<a href="" id="spoolercopyfileevent"></a>[**SpoolerCopyFileEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-spoolercopyfileevent)  
サーバーのスプーラとクライアントのスプーラーの両方でとも呼ばれます、この関数は、特定のプリンターの接続に関連するイベントの発生を示すイベント コードを受け取ります。

ポイントと印刷の DLL は、これらの関数のみをエクスポートする必要がありますされません。 たとえば Mscms.dll、Microsoft の ICM コンポーネントで使用される、ICM API 関数のセットをエクスポートします。

指定することは他の Dll さらに、またはの代わりに、ポイントと印刷の DLL をエクスポートする**GenerateCopyFilePaths**と**SpoolerCopyFileEvent**します。 これを行うには、DLL のファイル名を割り当てる、**ファイル**レジストリ キーの代わりに、**モジュール**レジストリ キー。 (を参照してください[キューに固有のファイルをインストールする](installing-queue-specific-files.md))。

インストール後にアプリケーションが DLL の名前に配置サーバーのレジストリを呼び出して**SetPrinterDataEx**、後続のすべての呼び出しを**SetPrinterDataEx** DLL のへの呼び出しで発生する[ **SpoolerCopyFileEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-spoolercopyfileevent) COPYFILE の指定されたイベントのコードで関数を\_イベント\_設定\_プリンター\_DATAEX します。

下に表示するファイルとは異なり、**ファイル**レジストリ キー (を参照してください[キューに固有のファイルをインストールする](installing-queue-specific-files.md))、ポイントと印刷の DLL はコピーされません、プリント サーバーからクライアントにクライアントがプリンターに接続するとき. 代わりに、DLL は、クライアントに常駐プリント サーバーへの接続を既に行われたと見なされます。 その結果、DLL は、ポイント アンド プリントの機能に関連しない他の目的で使用できます。

クライアントで、ポイントと印刷の DLL をインストールするための 1 つのメソッドがでその名前を指定するには、[プリンター INF ファイル](printer-inf-files.md)依存ファイルとしてそのため、ファイルをコピーできます中に、クライアントのドライバーのディレクトリに[のダウンロードドライバー固有のファイル](downloading-driver-specific-files.md)します。

 

 




