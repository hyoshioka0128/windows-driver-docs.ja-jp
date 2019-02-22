---
title: UVC 1.0 と 1.1 UVC の違い
description: UVC 1.0 と 1.1 UVC の違い
ms.assetid: 5199fc4f-7bc2-4edb-bb52-cd2028756f64
keywords:
- USB ビデオ クラス ドライバー WDK AVStream のバージョンの違い
- USB ビデオ クラス ドライバー WDK AVStream、UVC 1.0 と 1.1 の UVC の違い
- ビデオのクラス ドライバー WDK の USB UVC 1.0 と 1.1 の UVC の違い
- UVC ドライバー WDK AVStream、UVC 1.0 と 1.1 の UVC の違い
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c8113d17cc94d9464d63da905122cf10f0c03df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549160"
---
# <a name="differences-between-uvc-10-and-uvc-11"></a>UVC 1.0 と 1.1 UVC の違い


Windows 7 または Windows の以前のバージョンを使用する UVC 準拠のハードウェアを設計するとき、UVC 1.0 および 1.1 をサポートしている間する必要があります。

UVC 1.1 に準拠しているデバイスを設定する必要があります、 **bcdUVC** 0x110 VC インターフェイス クラスに固有のフラグ。 さらに、省略可能な処理単位記述子が存在する場合、1.1 準拠のデバイスが、以下を実行します。

1.  追加、 **bmVideoStandards**処理ユニットの記述子フィールド。

2.  更新プログラム、 **bLength**処理単位のフィールド。

3.  Update **wTotalLength** PU 処理単位のサイズを反映するようにします。

次の表では、UVC 1.0 と 1.1 の違いをまとめたものです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>状況</th>
<th>記述子と要求/管理</th>
<th>フィールド</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>change</p></td>
<td><p>クラスに固有の VC インターフェイス</p></td>
<td><p><strong>bcdUVC</strong></p></td>
<td><p>1.1 で 0x110 1.0 0x100</p></td>
</tr>
<tr class="even">
<td><p>廃止されました。</p></td>
<td><p>クラスに固有の VC インターフェイス</p></td>
<td><p><strong>dwClockFrequency</strong></p></td>
<td><p>1.1 を使用していません。</p></td>
</tr>
<tr class="odd">
<td><p>change</p></td>
<td><p>処理ユニット</p></td>
<td><p><strong>bLength</strong></p></td>
<td><p>10 + n 1.1 で 9 + 1.0 n</p></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>処理ユニット</p></td>
<td><p><strong>bmVideoStandards</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>change</p></td>
<td><p>特定のクラスとインターフェイスの入力ヘッダー</p></td>
<td><p><strong>bmaControls(n)</strong></p></td>
<td><p>1.1 を使用していくつかの異なる方法でこれらのビットの&quot;プローブし、コミット&quot;</p></td>
</tr>
<tr class="even">
<td><p>change</p></td>
<td><p>特定のクラスとインターフェイスの出力ヘッダー</p></td>
<td><p><strong>bLength</strong></p></td>
<td><p>1.1 で 9+(p*n) 1.0 8</p></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>特定のクラスとインターフェイスの出力ヘッダー</p></td>
<td><p><strong>bControlSize</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>特定のクラスとインターフェイスの出力ヘッダー</p></td>
<td><p><strong>bmaControls(n)</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>廃止されました。</p></td>
<td><p>コントロールをインターフェイスします。</p></td>
<td><p><strong>VC_REQUEST_INDICATE_HOST_CLOCK_CONTROL</strong></p></td>
<td><p>SCR/PTS を使用して、デバイスのペイロードを 1.0 のデバイスの必須をサポートしているホスト</p></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>コントロールをインターフェイスします。</p></td>
<td><p><strong>GET_INFO</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>処理ユニット</p></td>
<td><p><strong>PU_DIGITAL_MULTIPLIER_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>処理ユニット</p></td>
<td><p><strong>PU_ANALOG_VIDEO_STANDARD_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>処理ユニット</p></td>
<td><p><strong>PU_ANALOG_LOCK_STATUS_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>change</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>wLength</strong></p></td>
<td><p>1.1 34、1.0 の 26</p></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>dwClockFrequency</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>bmFramingInfo</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>bPreferredVersion</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>bMinVersion</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>bMaxVersion</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>GET_INFO</strong> VS_PROBE_CONTROL の</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>ビデオのプローブとコミットの制御</p></td>
<td><p><strong>GET_INFO</strong> VS_COMMIT_CONTROL の</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>廃止されました。</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FORMAT_MPEG1</strong></p></td>
<td><p>任意の Windows オペレーティング システムでサポートされていません</p></td>
</tr>
<tr class="odd">
<td><p>廃止されました。</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FORMAT_MPEG2PS</strong></p></td>
<td><p>任意の Windows オペレーティング システムでサポートされていません</p></td>
</tr>
<tr class="even">
<td><p>廃止されました。</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FORMAT_MPEG4SL</strong></p></td>
<td><p>任意の Windows オペレーティング システムでサポートされていません</p></td>
</tr>
<tr class="odd">
<td><p>廃止されました。</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FORMAT_VENDOR</strong></p></td>
<td><p>任意の Windows オペレーティング システムでサポートされていません</p></td>
</tr>
<tr class="even">
<td><p>廃止されました。</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FRAME_VENDOR</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FORMAT_FRAME_BASED</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新規</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FRAME_FRAME_BASED</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新規</p></td>
<td><p>特定のクラスとインターフェイス</p></td>
<td><p><strong>VS_FORMAT_STREAM_BASED</strong></p></td>
<td></td>
</tr>
</tbody>
</table>

 

UVC 1.0 デバイスの場合は、MPEG2TS 形式記述子の長さは 7 です。 UVC 1.1 には、新しい 16 バイトの GUID フィールドが含まれているため、MPEG2TS 形式記述子の長さは 23 です。

したがって、23 バイトに MPEG2TS 記述子を更新する場合は、設定する必要も、 **bcdUVC** 0x110 VC インターフェイス クラスに固有のフラグ。

 

 




