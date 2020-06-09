---
title: バグチェック 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
description: VIDEO_ENGINE_TIMEOUT_DETECTED のバグチェックには、0x00000141 という値が指定されています。 これは、表示エンジンの1つが適切なタイミングで応答に失敗したことを示します。
ms.assetid: 0912495D-DE6D-4064-BD66-DA6145889821
keywords:
- バグチェック 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
- VIDEO_ENGINE_TIMEOUT_DETECTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_ENGINE_TIMEOUT_DETECTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f631919f9570959777b668543d5e587afd27cab7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534659"
---
# <a name="bug-check-0x141-video_engine_timeout_detected"></a>バグチェック 0x141: ビデオ \_ エンジンの \_ タイムアウトが \_ 検出されました


ビデオ \_ エンジンの \_ タイムアウトが検出された \_ バグチェックの値は0x00000141 です。 これは、表示エンジンの1つが適切なタイミングで応答に失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="video_engine_timeout_detected-parameters"></a>ビデオ \_ エンジンの \_ タイムアウトが \_ 検出されたパラメーター


| パラメーター | 説明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 内部 TDR 復旧コンテキスト (TDR recovery context) へのポインター (省略可能 \_ \_ )。 |
| 2         | 責任を持つデバイスドライバーモジュール (所有者タグなど) へのポインター。          |
| 3         | セカンダリドライバー固有のバケットキー。                                |
| 4         | 省略可能な内部コンテキスト依存データ。                                   |

 

<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
タグのセカンダリデータ {270a33fd3da647 60D-BA89-3c1bae21e39b} には、追加の TDR 関連データが含まれています。 データを表示するには、 [**enumtag**](-enumtag--enumerate-secondary-callback-data-.md)を使用します。

 

 




