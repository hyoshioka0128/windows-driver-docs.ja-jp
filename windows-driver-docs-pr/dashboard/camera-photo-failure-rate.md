---
title: カメラの写真キャプチャ エラー率
description: この測定値は、カメラ デバイスで写真機能の使用が失敗したインスタンスの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 605ab114189e5a34e665dd3441ca4ad1ff10dcbf
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017078"
---
# <a name="percent-of-camera-photo-capture-failures"></a>カメラの写真キャプチャ エラー率

## <a name="description"></a>説明

カメラのプレビューをメモリにキャプチャするために、ユーザーは写真を撮影して自分のマシンに保存できます。 写真の撮影プロセスが失敗したら、ユーザーは目的の画像をキャプチャすることができません。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|10 個のインスタンス|
|**合格基準**|失敗に終わった写真撮影インスタンスが 5% 以下|
|**測定 ID**|16998997|

## <a name="calculation"></a>計算

1. この測定値は、**カメラ デバイスで写真機能の使用が失敗したインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

     a. この測定では、単一のデバイスで複数の撮影インスタンスがカウントされる場合があります
     
2. インスタンスの種類:

    a. "*成功した撮影イベント = 0% の失敗*" 

        i. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PHOTO_TAKEN)
       ii. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PHOTO_SEQUENCE_STARTED)

    b. 失敗した撮影イベント = 100% の失敗

         i. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PHOTO_TAKEN) HRESULT !=0
        ii. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PHOTO_SEQUENCE_STARTED) HRESULT !=0
       iii. Timed Out

### <a name="final-calculation"></a>最終的な計算

"*カメラによる撮影の失敗率 = すべてのインスタンスの平均*"