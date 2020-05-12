---
title: WinML ランタイム エラーが発生しているデバイスの割合
description: この測定は、Windows Machine Learning の全体的な正常性と信頼性を監視します
ms.topic: article
ms.date: 4/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: c56160116074bfca2aae06a45fc341d0ce35da30
ms.sourcegitcommit: 346052538ec47cad391c968382ae567e9fc28244
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82908408"
---
# <a name="percent-of-device-with-winml-runtime-error"></a>WinML ランタイム エラーが発生しているデバイスの割合

## <a name="description"></a>説明

この測定は、Windows Machine Learning 機能の全体的な正常性と信頼性を監視します。

この測定の主な目的は、WinML ランタイム エラーが発生しているデバイスの割合を追跡することです。

この測定は、WinML ランタイム エラー テレメトリと WinML ProcessInfo テレメトリのみを使用します。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard|
|**期間**|30 日|
|**測定基準**|Machine|
|**最小母集団**|30 デバイス (信頼区間を使用)|
|**合格基準**|1% 未満|
|**測定 ID**|25419759|

## <a name="calculation"></a>計算

WinML ランタイム エラーのある 1 日あたりの個別のデバイス数を、WinML を使用した 1 日あたりの個別のデバイス数で割った数を使用する

測定値 = WinML ランタイム エラー テレメトリを送信した 1 日あたりの個別の DeviceId 数/ WinML ProcessInfo テレメトリを送信した 1 日あたりの個別の DeviceId 数
