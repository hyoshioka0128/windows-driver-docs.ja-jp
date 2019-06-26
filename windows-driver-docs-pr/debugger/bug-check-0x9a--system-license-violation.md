---
title: バグ チェック 0x9A SYSTEM_LICENSE_VIOLATION
description: SYSTEM_LICENSE_VIOLATION のバグ チェックでは、0x0000009a のエラーの値を持ちます。 このバグ チェックでは、ソフトウェア使用許諾契約に違反したことを示します。
ms.assetid: 742d864c-46f8-4d7f-8617-061c75fe833a
keywords:
- バグ チェック 0x9A SYSTEM_LICENSE_VIOLATION
- SYSTEM_LICENSE_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_LICENSE_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f98b9862567a1e95fae0bbb70ddd6440aad398de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361698"
---
# <a name="bug-check-0x9a-systemlicenseviolation"></a>バグ チェック 0x9A:システム\_ライセンス\_違反


システム\_ライセンス\_違反のバグ チェックが 0x0000009a のエラーの値を持ちます。 このバグ チェックでは、ソフトウェア使用許諾契約に違反したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="systemlicenseviolation-parameters"></a>システム\_ライセンス\_違反パラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"><p><strong>0:</strong>製品は、WinNT をする必要があります。</p>
<p><strong>1:</strong>製品が LanmanNT または修正する必要があります。</p></td>
<td align="left"><p>シリアル番号の一部</p></td>
<td align="left"><p>製品のオプションから、製品の最初の 2 つの文字を入力します。</p></td>
<td align="left"><p>オフラインの製品の種類の変更が試行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>ソース 1 から登録された評価時間</p></td>
<td align="left"><p>シリアル番号の一部</p></td>
<td align="left"><p>代替のソースから登録された評価時間</p></td>
<td align="left"><p>Microsoft Windows 評価単位の期間にオフラインでの変更が試行されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>Open のエラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>セットアップ キーを開くことができませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>キー参照エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>セットアップ キーから SetupType または SetupInProgress 値が見つからないのは、セットアップ モードを検出できなかったためです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>キー参照エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>SystemPrefix</strong>セットアップ キーの値がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>(セットアップ コードを参照してください)</p></td>
<td align="left"><p>ライセンス プロセッサに無効な値が見つかりました</p></td>
<td align="left"><p>正式にライセンスを付与されたプロセッサ数</p></td>
<td align="left"><p>オフラインでライセンスされたプロセッサの数の変更が試行されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>Open のエラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>ProductOptions</strong>キーを開くことができませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>読み取りエラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>ProductType</strong>値を読み取ることができませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>変更通知のエラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>変更通知<strong>ProductOptions</strong>できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>変更通知のエラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>変更通知<strong>SystemPrefix</strong>できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>NTW、システムは、NTS システムに変換されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>変更の失敗に関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>セットアップ キーの参照が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>変更の失敗に関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>オプションのプロダクト キーへの参照が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>開こうとすると<strong>ProductOptions</strong>ワーカー スレッドで失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>セットアップ キーを開けませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p><strong>0:</strong>失敗値の設定</p>
<p><strong>1:</strong>変更通知が失敗しました</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>セットアップ キーのワーカー スレッドでエラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p><strong>0:</strong>失敗値の設定</p>
<p><strong>1:</strong>変更通知が失敗しました</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>製品のオプションのキーのワーカー スレッドでエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>開くことができません、 <strong>LicenseInfoSuites</strong>スイートのキー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>クエリをできません、 <strong>LicenseInfoSuites</strong>スイートのキー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>メモリ割り当てのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>メモリの割り当てができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>リセットできません、 <strong>ConcurrentLimit</strong>スイートのキーの値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>スイート製品のライセンス キーを開けません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>リセットできません、 <strong>ConcurrentLimit</strong>スイート製品の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>Open のエラーに関連付けられている状態コード</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>変更通知を開始できません、 <strong>LicenseInfoSuites</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x19</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>スイートは、PDC をする必要があるシステムで実行されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>エラーに関連付けられている状態コード</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>スイートでは、列挙中にエラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ポリシーのキャッシュへの変更が試行されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Microsoft Windows オペレーティング システムでは、ソフトウェアのライセンス契約の違反を検出します。

ユーザーは、オフライン システムの製品の種類を変更または Windows の評価単位の試用期間を変更した可能性があります。 特定の違反に関する詳細については、パラメーター リストを参照してください。

 

 




