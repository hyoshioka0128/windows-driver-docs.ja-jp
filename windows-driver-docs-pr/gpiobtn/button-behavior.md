---
title: ボタンの動作
description: このトピックでは、ハードウェア ボタンの想定される動作について説明します。
ms.assetid: 057A4F21-3514-4CCA-BCE2-279E8228B5A9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e230e9d2f673fee3c6645d7a06898124b321b215
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393484"
---
# <a name="button-behavior"></a>ボタンの動作


このトピックでは、ハードウェア ボタンの想定される動作について説明します。

## <a name="span-idrequiredandoptionalbuttonsinwindows10spanspan-idrequiredandoptionalbuttonsinwindows10spanspan-idrequiredandoptionalbuttonsinwindows10spanrequired-and-optional-buttons-in-windows10"></a><span id="Required_and_optional__buttons_in_Windows_10"></span><span id="required_and_optional__buttons_in_windows_10"></span><span id="REQUIRED_AND_OPTIONAL__BUTTONS_IN_WINDOWS_10"></span>Windows 10 で必須およびオプション ボタン


<table>
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">オペレーティング システム/デバイス</td>
<td align="left">Power</td>
<td align="left">上のボリューム/ボリューム ダウン</td>
<td align="left">開始</td>
<td align="left">戻る/検索</td>
<td align="left">Camera</td>
<td align="left">回転ロック</td>
</tr>
<tr class="even">
<td align="left">Windows 10 Mobile</td>
<td align="left">必須</td>
<td align="left">必須</td>
<td align="left"><p>電話 WVGA ディスプレイを使用するために必要な</p>
<p>その他のデバイスの場合は省略可能</p></td>
<td align="left"><p>電話 WVGA ディスプレイを使用するために必要な</p>
<p>その他のデバイスの場合は省略可能</p></td>
<td align="left">省略可能</td>
<td align="left">サポートされていません</td>
</tr>
<tr class="odd">
<td align="left">Windows 10 デスクトップ エディション (Home、Pro、Enterprise、および Education)]、[タブレット</td>
<td align="left">必須</td>
<td align="left">必須</td>
<td align="left">省略可能</td>
<td align="left">サポートされていません</td>
<td align="left">サポートされていません</td>
<td align="left">省略可能</td>
</tr>
<tr class="even">
<td align="left">Windows 10 デスクトップ エディション/その他のデバイス</td>
<td align="left">必須</td>
<td align="left">キーボードが取り外し可能なデバイスの場合は必須。 その他のすべてのデバイスの省略可能。</td>
<td align="left">省略可能</td>
<td align="left">サポートされていません</td>
<td align="left">サポートされていません</td>
<td align="left">省略可能</td>
</tr>
</tbody>
</table>

 

ボタンの要件の詳細については。

-   Windows 10 Mobile、2.6 のセクションを参照してください、[ハードウェアの最小要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)します。
-   Windows 10 デスクトップ エディションの場合、セクション 3.6 を参照して、[ハードウェアの最小要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)します。

## <a name="span-idbuttonbehaviorinwindows10spanspan-idbuttonbehaviorinwindows10spanspan-idbuttonbehaviorinwindows10spanbutton-behavior-in-windows10"></a><span id="Button_behavior_in_Windows_10"></span><span id="button_behavior_in_windows_10"></span><span id="BUTTON_BEHAVIOR_IN_WINDOWS_10"></span>Windows 10 でボタンの動作


### <a name="span-idsinglebuttonbehaviorinwindows10spanspan-idsinglebuttonbehaviorinwindows10spanspan-idsinglebuttonbehaviorinwindows10spansingle-button-behavior-in-windows10"></a><span id="Single_button_behavior_in_Windows_10"></span><span id="single_button_behavior_in_windows_10"></span><span id="SINGLE_BUTTON_BEHAVIOR_IN_WINDOWS_10"></span>Windows 10 での 1 つのボタンの動作

Windows 10 デスクトップ エディションの Windows 10 Mobile の電源を押してボタンをクリックし、トグル オン/オフ切り替えオン/オフを押してリリースし起動シャット ダウン カーテン起動シャット ダウン カーテン長押しおよび保持ハード シャット ダウン ハードウェア リセット検索キーを押すとリリースがサポートされていません(有効な市場) で Cortana を起動すると Cortana の起動またはキーを押してを音声ボリュームでの検索がサポートされている検索プレス アンド ホールド Not とインクリメント ボリューム増分ボリューム キーを押してをリリースして、自動繰り返しボリューム インクリメント自動繰り返し音量増音量下げるキーを押してを保持デクリメント ボリューム デクリメント ボリューム プレス リリースし自動繰り返しボリューム デクリメント自動繰り返しボリューム デクリメント戻るキーを押してと前アプリ ページを閉じる/アプリ前アプリ ページを閉じる/アプリ キーを押してリリースおよび保持起動タスク スイッチャー起動スイッチャーが UI の開始スタート画面の表示のスタート画面の回転ロックがサポートされていませんを切り替えはサポートされていません (UI オプションがある) カメラのフォーカス カメラ アプリ (フォーカス) カメラでカメラの起動アプリケーション処理済みのカメラ アプリケーション起動のカメラ アプリによって処理済みのシャッター/写真を撮影
 

### <a name="span-idbuttoncombinationbehaviorinwindows10spanspan-idbuttoncombinationbehaviorinwindows10spanspan-idbuttoncombinationbehaviorinwindows10spanbutton-combination-behavior-in-windows10"></a><span id="Button_combination_behavior_in_Windows_10"></span><span id="button_combination_behavior_in_windows_10"></span><span id="BUTTON_COMBINATION_BEHAVIOR_IN_WINDOWS_10"></span>Windows 10 でボタンの組み合わせの動作

述べたように、Windows 10 でいくつかボタンの組み合わせが適用されます、[ボタン アーキテクチャの Windows 10](https://docs.microsoft.com/windows-hardware/drivers/hid/buttons)または Windows 8.1 のボタンのアーキテクチャ。 Windows 10 では他のボタンの組み合わせをすべては、いずれかのボタンのアーキテクチャに適用されます。 Windows 10 のアーキテクチャを使用して、ハードウェア ボタンを記述することをお勧めします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">ボタンの組み合わせ</td>
<td align="left">Windows 10 デスクトップ エディション</td>
<td align="left">Windows 10 Mobile</td>
</tr>
<tr class="even">
<td align="left">開始日 + 音量増</td>
<td align="left">画面を切り替えるナレーター</td>
<td align="left">画面を切り替えるナレーター (対応する容易さ、アクセスの設定を有効になっている) を指定します。</td>
</tr>
<tr class="odd">
<td align="left">開始日 + ボリューム ダウン</td>
<td align="left">スクリーン ショットします。</td>
<td align="left">サポートされていません</td>
</tr>
<tr class="even">
<td align="left">開始日 + 電源</td>
<td align="left">(Windows 8.1 のボタンのアーキテクチャを使用して) の場合のみの Ctrl + Alt + Del</td>
<td align="left">サポートされていません</td>
</tr>
<tr class="odd">
<td align="left">電力 + 音量増</td>
<td align="left">(Windows 10 のボタンのアーキテクチャを使用して) の場合のみスクリーン ショットします。</td>
<td align="left">スクリーン ショットします。</td>
</tr>
<tr class="even">
<td align="left">電力 + ボリューム ダウン</td>
<td align="left">(Windows 10 のボタンのアーキテクチャを使用して) の場合のみの Ctrl + Alt + Del</td>
<td align="left"><p>起動、Windows フィードバック アプリ</p>
<p>ハードウェアのリセット (後 10 秒)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idbuttonbehaviorinwindows81spanspan-idbuttonbehaviorinwindows81spanbutton-behavior-in-windows-81"></a><span id="button_behavior_in_windows_8.1"></span><span id="BUTTON_BEHAVIOR_IN_WINDOWS_8.1"></span>Windows 8.1 でボタンの動作


### <a name="span-idsinglebuttonbehaviorinwindows81spanspan-idsinglebuttonbehaviorinwindows81spanspan-idsinglebuttonbehaviorinwindows81spansingle-button-behavior-in-windows-81"></a><span id="Single_button_behavior_in_Windows_8.1"></span><span id="single_button_behavior_in_windows_8.1"></span><span id="SINGLE_BUTTON_BEHAVIOR_IN_WINDOWS_8.1"></span>Windows 8.1 での 1 つのボタンの動作

Windows 8.1 の Windows 8.1 Phone Power キーを押してボタンしリリースの切り替えオン/オフ切り替えオン/オフを押してと起動シャット ダウン カーテン起動シャット ダウン カーテン長押しの保持をハード シャット ダウン ハードウェア リセット検索キーを押すし、リリースが Cortana のキーを押して起動をサポートしていませんを保持し、保留しないキーを押してを音声ボリュームでの Cortana の起動をサポートしリリースの増分ボリューム増分ボリューム キーを押してと自動繰り返しボリューム インクリメント自動繰り返し音量増音量下げるキーを押してを保持しデクリメント ボリューム デクリメント ボリューム プレス リリースを保持自動繰り返しボリューム デクリメント自動繰り返しボリューム デクリメントしないバックアップがサポートには、切り替えスタート画面切り替えを開始画面の回転のロック リリースがサポートされています。回転回転をロックしないサポートされていません、カメラのフォーカスをロックしないサポートされていませんカメラの該当するシャッター該当します。
 

### <a name="span-idbuttoncombinationbehaviorinwindows81spanspan-idbuttoncombinationbehaviorinwindows81spanspan-idbuttoncombinationbehaviorinwindows81spanbutton-combination-behavior-in-windows-81"></a><span id="Button_combination_behavior_in_Windows_8.1"></span><span id="button_combination_behavior_in_windows_8.1"></span><span id="BUTTON_COMBINATION_BEHAVIOR_IN_WINDOWS_8.1"></span>Windows 8.1 でボタンの組み合わせの動作

|                     |                           |                               |
|---------------------|---------------------------|-------------------------------|
| ボタンの組み合わせ  | Windows 8.1               | Windows 8.1 Phone             |
| 開始日 + 音量増   | 画面を切り替えるナレーター | サポートされていません                 |
| 開始日 + ボリューム ダウン | スクリーン ショットします。           | サポートされていません                 |
| 開始日 + 電源       | Ctrl+Alt+Del              | サポートされていません                 |
| 電力 + 音量増   | サポートされていません             | スクリーン ショットします。               |
| 電力 + ボリューム ダウン | サポートされていません             | ハードウェアのリセット (後 10 秒) |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[Windows 10 のボタンのアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/hid/buttons)  
[最小ハードウェア要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)  



