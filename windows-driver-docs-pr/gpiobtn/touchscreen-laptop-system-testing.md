---
title: タッチスクリーン ノート PC システム テスト
description: このトピックでは、タッチ スクリーンのラップトップ システムのテストについて説明します。
ms.assetid: 0DD7865F-C31C-48AD-8775-4AC1E469176F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf95ec0a0826da32f61aac4cfce28a67a25cc5b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571340"
---
# <a name="touchscreen-laptop-system-testing"></a>タッチスクリーン ノート PC システム テスト


このトピックでは、タッチ スクリーンのラップトップ システムのテストについて説明します。

**スクリーン キーボードの配置 (タッチ スクリーン ラップトップ システムのみ)**

1.  システムの電源し、に移動、**開始**画面。
2.  実行[タッチ キーボードの配置手順](indicator-testing.md#touchkbd)します。

    *検証*:スクリーン キーボードはデプロイする必要があります。

3.  システム (縦と横) を回転します。

    *検証*:画面の向きを変更しないでください。

## <a name="span-iddockingstationtestingspanspan-iddockingstationtestingspanspan-iddockingstationtestingspandocking-station-testing"></a><span id="Docking_station_testing"></span><span id="docking_station_testing"></span><span id="DOCKING_STATION_TESTING"></span>ドッキング ステーションのテスト


**システムをスレート モード (コンバーチブル ドッキング システムのみ) でのドッキング**

1.  使用可能なシステムのドッキング (スレート デバイスには、キーボードがあるない場合に接続された USB キーボード) が GPIO があります。 ドッキングとラップトップ/スレートの変換を区別する、[変換のスレートのラップトップとドッキング](docking-versus-laptop-slate-conversion.md)を参照してください。 コンバーチブル、スレート モードでシステムを構成する。 (を参照してください[スレート/ラップトップ モード変換手順](indicator-testing.md#conv))。
2.  スレート モードでシステムを起動し、ドッキング システムにアタッチします。
3.  実行[タッチ キーボードの配置手順](indicator-testing.md#touchkbd)します。

    *検証*:スクリーン キーボードを展開する必要があります。

4.  システム (縦と横) を回転します。

    *検証*:画面の向きを変更しないでください。

## <a name="span-idphysicalbuttonstestingspanspan-idphysicalbuttonstestingspanspan-idphysicalbuttonstestingspanphysical-buttons-testing"></a><span id="Physical_buttons_testing"></span><span id="physical_buttons_testing"></span><span id="PHYSICAL_BUTTONS_TESTING"></span>物理ボタンのテスト


システムでは、次のユーザーにボタンのセットを公開できます。

-   電源 ボタン - 必須
-   ボリューム ボタン - 必須の +/-
-   Windows ボタン - 必須
-   回転ロック ボタン - オプション

**ボタンの動作**

-   ボタンに、次の表に記載されているボタンの組み合わせごとに、すべてのケースで想定される動作が発生したことを検証します。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">ボタンまたは組み合わせ</th>
    <th align="left">キーを押してエクスペリエンス</th>
    <th align="left">長押ししますエクスペリエンス</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left">Windows</td>
    <td align="left">スタート画面に移動します</td>
    <td align="left">N/A</td>
    </tr>
    <tr class="even">
    <td align="left">音量増</td>
    <td align="left">音量を上げる</td>
    <td align="left">迅速なボリュームの増加</td>
    </tr>
    <tr class="odd">
    <td align="left">音量-</td>
    <td align="left">音量を下げる</td>
    <td align="left">迅速なボリュームの減少</td>
    </tr>
    <tr class="even">
    <td align="left">回転ロック</td>
    <td align="left">回転ロックの切り替え</td>
    <td align="left">N/A</td>
    </tr>
    <tr class="odd">
    <td align="left">Power</td>
    <td align="left">コネクト スタンバイの電源を入れます</td>
    <td align="left"><p>スタンバイ システムの接続</p>
    <ul>
    <li>HoldTime&lt;2 s: CS を入力します。</li>
    <li>2&lt;= HoldTime&lt;= 10: UX の電源を切りますスライド</li>
    <li>HoldTime&gt;数十: 電源オフ</li>
    </ul>
    <p>接続されていないスタンバイ システム</p>
    <ul>
    <li>Holdtime&lt; 4 s: スリープ状態の [オプション]</li>
    <li>Holdtime&gt;= 4 s: 電源オフ、デバイス</li>
    </ul></td>
    </tr>
    <tr class="even">
    <td align="left">Windows + 音量増</td>
    <td align="left">ナレーターを終了または起動</td>
    <td align="left">N/A</td>
    </tr>
    <tr class="odd">
    <td align="left">Windows + ボリューム ダウン</td>
    <td align="left">画面キャプチャを実行します。</td>
    <td align="left">N/A</td>
    </tr>
    <tr class="even">
    <td align="left">Windows + 電源</td>
    <td align="left">セキュリティ シーケンス (ロック画面の表示)</td>
    <td align="left">N/A</td>
    </tr>
    </tbody>
    </table>

     

 

 




