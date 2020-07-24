---
title: カメラのプレビュー エラー率
description: この測定値は、カメラ デバイスでプレビュー機能の使用が失敗したインスタンスの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: d0cfdc6b7cc7b4713fbf9eccc2c477c630f01605
ms.sourcegitcommit: 191da92cfb33775b02ca160b4657d409635bd60c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86898734"
---
# <a name="percent-of-camera-preview-failures"></a>カメラのプレビュー エラー率

## <a name="description"></a>説明

画像をキャプチャしようとすると、デバイスではキャプチャ対象の画像をプレビューします。 プレビュー機能が失敗すると、ユーザーはカメラの映像を見ることができず、画像をキャプチャして写真として保存することができない可能性があります。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|10 個のインスタンス|
|**合格基準**|失敗に終わったプレビュー インスタンスが 8% 以下|
|**測定 ID**|16998893|

## <a name="calculation"></a>計算

1. この測定値は、**カメラ デバイスでプレビュー機能の使用が失敗したインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

   a。 この測定では、単一のデバイスで複数のプレビュー インスタンスがカウントされる場合があります。

2. インスタンスの種類:

   a。 "*成功したプレビュー イベント = 0% の失敗*"

```cpp
MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STARTED) HRESULT == 0
MFCaptureEnginePreviewSinkFirstFrame (MF_CAPTURE_ENGINE_PREVIEW_STARTED)
```

   b. "*失敗したプレビュー イベント = 100% の失敗*"

```cpp
MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STARTED) HRESULT != 0
```

**または**、成功したプレビュー イベントの後に以下が続く場合:

```cpp
MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_ERROR)
MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STOPPED) > 1000ms
MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STARTED) HRESULT != 0
```

### <a name="final-calculation"></a>最終的な計算

"*カメラのプレビューの失敗率 = すべてのインスタンスの平均*"
