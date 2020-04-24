---
title: カメラのビデオおよびストリーム エラー率
description: この測定値は、カメラ デバイスでビデオおよびストリーミング機能の使用が失敗したインスタンスの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1365dc8641cb6a5b4d7d0bd8f9856c281c368174
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017075"
---
# <a name="percent-of-camera-video-and-stream-failures"></a>カメラのビデオおよびストリーム エラー率

## <a name="description"></a>説明

カメラのビデオ ストリームをキャプチャするには、マシンの映像をビデオ ファイルに継続的に格納する必要があります。 ビデオおよびストリーミング機能が失敗すると、ユーザーはカメラの映像をキャプチャすることができず、保存されていないビデオが失われる可能性があります。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|10 個のインスタンス|
|**合格基準**|失敗に終わったビデオおよびストリーミング インスタンスが 10% 以下|
|**測定 ID**|16999057|

## <a name="calculation"></a>計算

1. この測定値は、**カメラ デバイスでビデオおよびストリーミング機能の使用が失敗したインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

   a。 この測定では、単一のデバイスで複数のビデオおよびストリーミング インスタンスがカウントされる場合があります。

2. インスタンスの種類:

   a。 "*成功したビデオおよびストリーミングのイベント = 0% の失敗*"  

       i. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_RECORD_STARTED)

   b. "*失敗したビデオおよびストリーミングのイベント = 100% の失敗*"

         i. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_ERROR)
        ii. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_RECORD_STOPPED)
       iii. MFCaptureEngineSessionStop
        iv. OnEvent_RecordStop_Failure
         v. Timed Out

### <a name="final-calculation"></a>最終的な計算

"*カメラのビデオおよびストリーミングの失敗率 = すべてのインスタンスの平均*"