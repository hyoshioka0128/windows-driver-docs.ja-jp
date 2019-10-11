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
ms.openlocfilehash: d5bc5812549e86480da6d905d8364601c03b7133
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038100"
---
# <a name="bug-check-0x141-video_engine_timeout_detected"></a>バグ チェック 0x141:VIDEO @ NO__T-0ENGINE @ NO__T-1TIMEOUT @ NO__T-2DETECTED


ビデオ @ no__t-0ENGINE @ no__t-1TIMEOUT @ no__t-2DETECTED されたバグチェックの値は0x00000141 です。 これは、表示エンジンの1つが適切なタイミングで応答に失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="video_engine_timeout_detected-parameters"></a>VIDEO @ no__t-0ENGINE @ no__t-1TIMEOUT @ no__t-2DETECTED されたパラメーター


| パラメーター | 説明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | TDR の内部復旧コンテキストへのポインター (TDR @ no__t-0RECOVERY @ no__t-1CONTEXT)。 |
| 2         | 責任を持つデバイスドライバーモジュール (所有者タグなど) へのポインター。          |
| 3         | セカンダリドライバー固有のバケットキー。                                |
| 4         | 省略可能な内部コンテキスト依存データ。                                   |

 

<a name="remarks"></a>コメント
-------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
タグのセカンダリデータ {270a33fd3da647 60D-BA89-3c1bae21e39b} には、追加の TDR 関連データが含まれています。 データを表示するには、 [**enumtag**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-enumtag--enumerate-secondary-callback-data-)を使用します。

 

 




