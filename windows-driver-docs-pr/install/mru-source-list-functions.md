---
title: MRU ソースの取得関数
description: MRU ソースの取得関数
ms.assetid: 62c6b144-5883-45cf-a114-7b82453f275f
keywords:
- SetupAPI 関数 WDK では、最近使用したソースを一覧表示します。
- 最近使用したソースには、WDK SetupAPI が一覧表示されます。
- 最近使用したソースには、WDK SetupAPI が一覧表示されます。
- ソースの WDK MRU 一覧します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bc98834f1d552ca3bd37399747fdf62ba1b2b0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366682"
---
# <a name="mru-source-list-functions"></a>MRU ソースの取得関数





最近使用 (した MRU) のソース リストがユーザーのコンピューターに常駐であり、以前のインストールで使用するソース パスに関する情報が含まれます。 この情報は、ソース パスのユーザーの入力を求めるときに使用できます。

*デバイス インストール アプリケーション*ユーザー固有のソースの一覧にアクセスできると、アプリケーションがある管理者権限、システム全体のソースの一覧。 デバイスのインストール アプリケーションでは、デバイスのインストール アプリケーションの終了時に破棄される一時的なソースのリストも作成できます。 呼び出して**SetupSetSourceList**デバイスのインストール アプリケーションは、インストール中に使用されるソース リストを識別します。

次の表には、ソース リストを操作するために使用できる関数が一覧表示します。 関数の詳細な説明については、Microsoft Windows SDK のドキュメントを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddtosourcelista" data-raw-source="[&lt;strong&gt;SetupAddToSourceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupaddtosourcelista)"><strong>SetupAddToSourceList</strong></a></p></td>
<td align="left"><p>ソースの一覧にエントリを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcanceltemporarysourcelist" data-raw-source="[&lt;strong&gt;SetupCancelTemporarySourceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcanceltemporarysourcelist)"><strong>SetupCancelTemporarySourceList</strong></a></p></td>
<td align="left"><p>一時的なリストのキャンセルを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupfreesourcelista" data-raw-source="[&lt;strong&gt;SetupFreeSourceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupfreesourcelista)"><strong>SetupFreeSourceList</strong></a></p></td>
<td align="left"><p>以前の呼び出しによって割り当てられたリソースを解放<a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetsourcelista" data-raw-source="[&lt;strong&gt;SetupSetSourceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetsourcelista)"> <strong>SetupSetSourceList</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupquerysourcelista" data-raw-source="[&lt;strong&gt;SetupQuerySourceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupquerysourcelista)"><strong>SetupQuerySourceList</strong></a></p></td>
<td align="left"><p>現在のインストール ソースの一覧を照会します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremovefromsourcelista" data-raw-source="[&lt;strong&gt;SetupRemoveFromSourceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremovefromsourcelista)"><strong>SetupRemoveFromSourceList</strong></a></p></td>
<td align="left"><p>インストール元の一覧からエントリを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetsourcelista" data-raw-source="[&lt;strong&gt;SetupSetSourceList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetsourcelista)"><strong>SetupSetSourceList</strong></a></p></td>
<td align="left"><p>システムの MRU 一覧、ユーザーの MRU 一覧または一時的なリストには、インストール ソースの一覧を設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





