---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_クリア
description: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_KSPROPERTY で定義されているプロパティのクリア ID\_CAMERACONTROL\_PERFRAMESETTING\_プロパティを使用して、クリアしますフレームごとのドライバーの設定。
ms.assetid: CCFB4226-36A7-4A5A-8A65-F8E9F281AAA4
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CLEAR ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CLEAR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5cf0889ed1e914bfbafb63aef2a4f2077ba6d58b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582183"
---
# <a name="kspropertycameracontrolperframesettingclear"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_クリア

**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_クリア**で定義されているプロパティ ID **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_プロパティ**ドライバーでフレームごとの設定を消去するために使用します。 これは、制御の設定のみであり、このペイロードはありません。 これは通常の終了中に使用されます (準備の解除中)、写真のシーケンス。

## <a name="photo-sequence-usage-summary"></a>フォト シーケンス使用状況の概要


**無限の写真のシーケンス**

準備状態は、準備の写真の sequence コマンドが、アプリのクライアントによって発行されたときに、写真のシーケンスになります。 ドライバーの暗証番号 (pin) が作成される可能性がありますまたはウォーム スタート状態によっては既に作成されて、写真シーケンスは準備が初めてかどうか。 準備状態が完了した後、ドライバーの暗証番号 (pin) は実行中の状態と、準備完了状態に写真のシーケンスの転送に通過しました。 ドライバーは、その内部履歴バッファー入力し、開始されます。

写真のシーケンスの開始後にトリガー KS\_VideoControlFlag\_StartPhotoSequenceCapture を受信し、状態のキャプチャには、写真のシーケンスが移行され、ドライバーの暗証番号 (pin) は実行中の状態を維持します。 この状態を入力すると、ドライバーは、将来のフレームを入力し、将来のフレームとすべての利用可能な履歴フレームを提供が開始されます。

写真のシーケンスの停止後にトリガー KS\_VideoControlFlag\_StopPhotoSequenceCapture が受信した、写真のシーケンスが準備完了状態に言わおよびドライバーの暗証番号 (pin) が実行状態のままになります。 この状態を入力するには、ドライバーはフレームをパイプラインに配信しないようにし、代わりに、内部履歴バッファーの入力を開始します。

Unprepare 状態は、アプリのクライアントによって終了コマンドが発行されたときに、写真のシーケンスになります。 ドライバーの暗証番号 (pin) は、ウォームの状態が有効かどうかによって、パイプラインによって停止または一時停止状態に、実行中の状態から通過したするされます。

**写真の有限のシーケンス**

準備状態は、準備の写真の sequence コマンドが、アプリのクライアントによって発行されたときに、写真のシーケンスになります。 ドライバーの暗証番号 (pin) が作成される可能性がありますまたはウォーム スタート状態によっては既に作成されて、写真シーケンスは準備が初めてかどうか。 準備状態が完了した後、ドライバーの暗証番号 (pin) は実行中の状態と、準備完了状態に写真のシーケンスの転送に通過しました。 ドライバーは、その内部履歴バッファー入力し、開始されます。

写真のシーケンスの開始後にトリガー KS\_VideoControlFlag\_StartPhotoSequenceCapture を受信し、状態のキャプチャには、写真のシーケンスが移行され、ドライバーの暗証番号 (pin) は実行中の状態を維持します。 この状態を入力すると、ドライバーは、将来のフレームを入力し、将来のフレームとすべての利用可能な履歴フレームを提供が開始されます。

写真に指定された最後のフレームの後にシーケンスが付けられた KSSTREAM\_ヘッダー\_OPTIONSF\_ENDOFPHOTOSEQUENCE フォト シーケンスは、配信の待機状態にそれと同じし、ドライバーの暗証番号 (pin) のままで、実行状態。 この状態を入力すると、ドライバーはすべてのフレームをパイプラインに配信を停止します。 ドライバーのフレームを生成しないこと、またはその内部履歴バッファー入力を開始することもできます。 正確な動作は、OEM の責任です。

写真のシーケンスの停止後にトリガー KS\_VideoControlFlag\_StopPhotoSequenceCapture が受信した、写真のシーケンスが準備完了状態に言わおよびドライバーの暗証番号 (pin) が実行状態のままになります。 この状態を入力するには、ドライバーは、パイプラインに配信されたフレームなしでその内部履歴バッファーを入力を開始します。

Unprepare 状態は、アプリのクライアントによって終了コマンドが発行されたときに、写真のシーケンスになります。 ドライバーの暗証番号 (pin) は、ウォームの状態が有効か無効かどうかに応じて、パイプラインによって停止または一時停止状態に、実行中の状態から通過したするされます。

## <a name="requirements"></a>必要条件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
