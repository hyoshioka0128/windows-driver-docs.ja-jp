---
ms.assetid: ACD6E5C3-5CE5-4C3F-BA44-1C87C39EF3C4
title: Windows 10 のドライバーの収束モデル
description: Windows 10 より前のリリースの Windows と Windows Phone にデバイスを対応させるには、多くの場合、2 つの異なるドライバーを作成する必要がありました。たとえば、Windows 8.1 用のドライバーと Windows Phone 8.1 用のドライバーが必要となりました。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0195d6ebc13009f06de34fe78fda4606b020f65c
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63357590"
---
# <a name="driver-convergence-model-for-windows10"></a>Windows 10 のドライバーの収束モデル

Windows 10 より前のリリースの Windows と Windows Phone にデバイスを対応させるには、多くの場合、2 つの異なるドライバーを作成する必要がありました。たとえば、Windows 8.1 用のドライバーと Windows Phone 8.1 用のドライバーが必要となりました。 Windows 10 では、ほとんどの場合、あらゆるバージョンの Windows 10 で動作する 1 つのドライバーを作成できます。 ここでは、Windows 10 におけるデバイス ドライバー インターフェイスの収束プランについて説明します。また、バージョン固有の相違点がある場合は、その相違点についても詳しく説明します。 この説明によって、次の質問の回答が導き出されます。

-   レガシ ドライバーの場合、Windows 8.1 のドライバーは Windows 10 デスクトップ エディション (Home、Pro、Enterprise) や Windows 10 Mobile で動作しますか。
-   新しいドライバーの場合、Windows 10 キットを使用して、Windows 10 デスクトップ エディションと Windows 10 Mobile で動作する 1 つのドライバーをビルドできますか。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テクノロジ</th>
<th align="left">Windows 8.1 のドライバーのバイナリが Windows 10 で動作するかどうか</th>
<th align="left">Windows 10 での変更点</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">オーディオ</td>
<td align="left">〇</td>
<td align="left"><p>Windows 10 以降では、PnP、電源管理、およびアイドル状態の管理のために KMDF インターフェイスを呼び出すカーネルモード ドライバー フレームワーク (KMDF) オーディオ ドライバーを作成できます。 I/O 処理の場合、KMDF オーディオ ドライバーでは WDF の I/O キュー機能を使用できませんが、PortClass が提供する既存の COM インターフェイスを代わりに使用する必要があります。 ただし、タイマー、割り込み、DMA、リモート I/O ターゲットについてはフレームワークのサポートを利用できます。 KMDF オーディオ ドライバーは、Windows 10 デスクトップ エディションと Windows 10 Mobile の両方で動作します。</p>
<p>PortClass にリンクする Windows 8.1 の既存のドライバーは、Windows 10 デスクトップ エディションと Windows 10 Mobile で引き続き動作します。</p></td>
</tr>
<tr class="even">
<td align="left">生体認証</td>
<td align="left">〇</td>
<td align="left"><p>Windows 生体認証フレームワーク (WBF) は、Windows 10 デスクトップ エディションと Windows 10 Mobile の両方で利用できます。</p>
<p>Windows 10 Mobile 用の新しい生体認証ドライバーを開発する場合は、Windows 8.1 の WBF ドライバーを出発点として使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left">Bluetooth</td>
<td align="left">〇</td>
<td align="left"><p>Windows 10 では、すべてのデバイスに対する Bluetooth トランスポート ドライバー インターフェイスが収束され、ユニバーサル Bluetooth ドライバー モデルが使用されます。 つまり、すべての Windows デバイス プラットフォームで動作する単一のドライバーを作成できます。</p>
<p>Bluetooth オーディオ ドライバーの表層部は Windows 10 用に分かれ、次の 2 つのオプションを選択できるようになっています。</p>
<ul>
<li>デスクトップとモバイル デバイスの両方で動作する新しいユニバーサル オーディオ ドライバーを記述できます。</li>
<li>既存の Windows Phone 8.1 Bluetooth オーディオ ドライバーは、Windows 10 Mobile でも動作します。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left">Camera</td>
<td align="left">〇</td>
<td align="left"><p>Windows Phone 8.1 で提供されていた機能 (オートフォーカスや HFR など) は、Windows 10 デスクトップ エディションと Windows 10 Mobile の両方で使用できます。 Windows 8.1 のレガシ カメラ ドライバーでこれらの機能を利用するには、ドライバーの変更が必要になります。</p></td>
</tr>
<tr class="odd">
<td align="left">Cellular</td>
<td align="left">〇</td>
<td align="left"><p>Windows 10 では、PC でデータ カード向けの MBIM 1.0 (モバイル ブロードバンド インターフェイス モデル) が引き続きサポートされます。</p>
<p>収束済みのスタックを使用した携帯電話と Wi-Fi 接続の管理に相当します。 携帯電話会社は、移動体通信設定の Open Mobile Alliance Device Management (OMA DM) 構成を Windows 10 デスクトップ エディションと Windows 10 Mobile の両方で使用できます。 また、OEM は、Windows 10 デスクトップ エディションと Windows 10 Mobile の両方でマルチバリアント プロビジョニングにアクセスできます。Windows 10 デスクトップ エディションでは、モバイル ブロードバンド アカウント エクスペリエンス (MBAE) を引き続き使用できます。</p></td>
</tr>
<tr class="even">
<td align="left">ディスプレイ</td>
<td align="left">〇</td>
<td align="left"><p>既に収束されています。 Windows 8.1 と Windows Phone 8.1 では、Windows Display Driver Model (WDDM) 1.3 が動作します。 WDDM 1.3 は Windows 10 で引き続きサポートされます。 WDDM 2.0 は Windows 10 の新機能です。 Direct3D (D3D) 12 ランタイムと機能を使用するには、WDDM 2.0 ドライバーが必要です。</p></td>
</tr>
<tr class="odd">
<td align="left">Location</td>
<td align="left">〇</td>
<td align="left"><p>Windows 10 用の新しい GNSS (全地球航法衛星システム) アダプター DDI。</p>
<p>GNSS のレガシ PE を使用して Windows 8.1 センサーがサポートされます。</p></td>
</tr>
<tr class="even">
<td align="left">NFC</td>
<td align="left">〇</td>
<td align="left"><p>スマート カード、Radio Manager、SE 用の新しい Windows 10 DDI。</p>
<p>Windows 8.1 NFC ドライバーは引き続き動作しますが、新機能を利用することはできません。</p></td>
</tr>
<tr class="odd">
<td align="left">センサー</td>
<td align="left">〇</td>
<td align="left"><p>Windows 10 用の新しいドライバーでは、共通のセンサー スタックを使用するユーザー モード ドライバー フレームワーク (UMDF) 2.<em>x</em> ドライバー (Windows Phone 8.1 モデルと同様のもの) を作成できます。Windows 10 デスクトップ エディションと Windows 10 Mobile で同じドライバー パッケージが動作します。</p>
<p>Windows 8.1 センサー クラス拡張機能では UMDF 1 が使われます。 Windows Phone 8.1 センサー クラス拡張機能では UMDF 2 が使われます。 Windows 10 の新しいセンサー クラス拡張機能では、Windows Phone 8.1 と同様に UMDF 2 が使われます。 Windows 10 キットを使用してビルドするには、後者を使用する必要があります。 Windows 8.1 のドライバーのバイナリは Windows 10 でも動作します。 Windows 10 用の HID クラス ドライバーも引き続き用意されているため、Windows 8.1 の定義済みの既存の HID タイプを使用する場合は、ベンダーでドライバーを提供したり、ファームウェアを変更したりする必要はありません。</p></td>
</tr>
<tr class="even">
<td align="left">タッチ/高精度タッチパッド (PTP)</td>
<td align="left">〇</td>
<td align="left"><p>Windows 10 では、HID とタッチの両方のミニポート ドライバーがサポートされます。 ベンダーは、レガシ HID ドライバーを更新することも、新しいタッチ ミニポート ドライバーを実装することもできます。</p>
<p>Windows 10 Mobile では、USB と I2C に限定されていたバスの制限が排除されました。 現在のクラス ドライバーはそのまま維持され、その他のバスには HID ミニポート ドライバーが必要です。 カスタム ジェスチャをサポートするためにフィルター ドライバーを提供できます。</p></td>
</tr>
<tr class="odd">
<td align="left">USB</td>
<td align="left">〇</td>
<td align="left"><p>Windows 8.1 はホスト コントローラー スタックを提供します。 Windows 10 は、ホスト コントローラーを搭載したデバイス (PC、タブレット PC、モバイル) が周辺機器として動作できるようにするためのファンクション スタックを追加します。</p></td>
</tr>
<tr class="even">
<td align="left">Windows Driver Framework (WDF)</td>
<td align="left">〇</td>
<td align="left"><p>Windows 10 には、KMDF 1.15、UMDF 2.15、UMDF 1.11、および以前のバージョンのフレームワークが付属しています。 また、Windows 10 Mobile にも、KMDF 1.15、UMDF 2.15、および以前のバージョンのフレームワークが付属しています。 ただし、UMDF Version 1 は Windows 10 Mobile では利用できません。 <a href="getting-started-with-universal-drivers.md" data-raw-source="[Universal Windows drivers](getting-started-with-universal-drivers.md)">ユニバーサル Windows ドライバー</a>の作成に使用できるのは、KMDF と UMDF Version 2 だけです。</p></td>
</tr>
<tr class="odd">
<td align="left">WLAN</td>
<td align="left">〇</td>
<td align="left"><p>WDI (WLAN デバイス ドライバー インターフェイス) は、Windows 10 用の新しいユニバーサル WLAN ドライバー モデルです。 WLAN デバイスの製造元は、単一の WDI ミニポート ドライバーを作成して、すべてのデバイス プラットフォームで実行することができます。これに必要なコードは、前のネイティブ WLAN ドライバー モデルよりも少なくなります。 Windows 10 で導入されるすべての新しい WLAN 機能には WDI ベースのドライバーが必要です。</p>
<p>ベンダーから提供されるネイティブ WLAN ドライバーは Windows 10 で引き続き動作しますが、開発時に対象とした Windows バージョンの機能に限定されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





