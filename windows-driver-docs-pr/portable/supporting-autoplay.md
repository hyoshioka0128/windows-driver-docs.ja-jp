---
Description: 自動再生のサポート
title: 自動再生のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2236bccd98008dadffbb349c988caac1e65c42
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464092"
---
# <a name="supporting-autoplay"></a>自動再生のサポート


自動再生は、ポータブル デバイスでコンテンツを検出するシェルの機能です。 現在の自動再生の設定によっては、この機能は、ファイルの標準のフォルダー ビューを表示する、ハンドラーの使用可能なアプリケーションの一覧を表示するなど、いくつかの操作のいずれかを実行など。

WPD デバイスがサポートされているコンテンツの種類の一覧を提供できるように、Windows Vista で自動再生機能が拡張されました。 同様に、WPD アプリケーションでは、サポートされるコンテンツの種類を登録できます。 (詳細については、アプリケーションの登録、WPD SDK を参照してください)。

## <a name="span-idthewpdautoplayschemespanspan-idthewpdautoplayschemespanspan-idthewpdautoplayschemespanthe-wpd-autoplay-scheme"></a><span id="The_WPD_AutoPlay_Scheme"></span><span id="the_wpd_autoplay_scheme"></span><span id="THE_WPD_AUTOPLAY_SCHEME"></span>WPD 自動再生の構成


WPD 自動再生のスキームは、Windows Vista の自動再生の機能と統合します。 これは、次の表で説明されている 3 つの自動再生カテゴリをサポートすることで。

| カテゴリ | 説明                                                                                                         |
|----------|---------------------------------------------------------------------------------------------------------------------|
| ソース   | WPD デバイスは、コンテンツのソースとして扱うことが、デバイスからは、コンテンツを転送できます。        |
| シンク     | WPD デバイスは、コンテンツの保存先として扱うことが、デバイスには、コンテンツを転送できます。    |
| 関数 | たとえば、送信して SMS メッセージを受信、WPD デバイスは、プログラミング可能なまたは制御可能な機能をサポートします。 |

 

これらのカテゴリをサポートするデバイスはデバイスに適切なエントリを設定する必要があります\_セットアップ情報 (.inf) ファイルの [AddReg] セクション。 WPD クラスのインストーラーでサポートされている 2 つの自動再生ディレクティブを次の表に示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">セクション</th>
<th align="left">ディレクティブまたはパラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">AutoPlaySourceOnly</td>
<td align="left">このディレクティブは、自動再生のソースとしてのみ動作するデバイスに必要です。
<ul>
<li>Reg のルートは、"HKR"である必要があります。</li>
<li>種類は 0x10001 である必要があります。</li>
<li>1 の値を設定する必要があります。</li>
</ul>
<p>例:</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"AutoPlaySourceOnly",0x10001,1</code></p></td>
</tr>
<tr class="even">
<td align="left">Device_AddReg</td>
<td align="left">EnableDefaultAutoPlaySupport ディレクティブ</td>
<td align="left">このディレクティブが必要です。
<ul>
<li>Reg のルートは、"HKR"である必要があります。</li>
<li>種類は 0x10001 である必要があります。</li>
<li>有効な値 (0 または 1) を設定する必要があります。</li>
</ul>
<p>例:</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableDefaultAutoPlaySupport",0x10001,1</code></p></td>
</tr>
</tbody>
</table>

 

ほとんどのデバイスでは、そのセットアップ情報ファイルで EnableDefaultAutoPlaySupport ディレクティブを指定します。 AutoPlaySourceOnly ディレクティブは、双方向の送信をサポートしていないレガシ デバイスにのみ提供されます。

自動再生に参加するデバイスしたくない場合は、EnableAutoPlaySupport ディレクティブを 0 に設定またはドライバーのセットアップ情報 (.inf) ファイルからこのディレクティブを省略します。 明示的に指定された WPD デバイスの自動再生機能を無効にする必要がある場合はこれを行うデバイスで false DeviceHandlers 値を作成して\_.inf ファイルの Parameters セクション。

カスタムの自動再生設定を作成する場合は、これを行うデバイスで秘密 DeviceHandlers 値を作成して\_セットアップ情報 (.inf) ファイルの Parameters セクション。

 

 




