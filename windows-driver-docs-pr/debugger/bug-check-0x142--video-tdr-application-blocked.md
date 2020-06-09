---
title: バグチェック 0x142 VIDEO_TDR_APPLICATION_BLOCKED
description: VIDEO_TDR_APPLICATION_BLOCKED のバグチェックの値は0x00000142 です。 これは、アプリケーションがグラフィックスハードウェアへのアクセスをブロックされていることを示します。
ms.assetid: B97FCA51-C368-4144-A364-50135A8DE836
keywords:
- バグチェック 0x142 VIDEO_TDR_APPLICATION_BLOCKED
- VIDEO_TDR_APPLICATION_BLOCKED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_TDR_APPLICATION_BLOCKED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 513401c67dfdb002eabb2df4df0da49bf5bbf967
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534657"
---
# <a name="bug-check-0x142-video_tdr_application_blocked"></a>バグチェック 0x142: VIDEO \_ TDR \_ APPLICATION は \_ ブロックされています


VIDEO TDR アプリケーションのブロックされたバグチェックには、 \_ \_ \_ 値0x00000142 があります。 これは、アプリケーションがグラフィックスハードウェアへのアクセスをブロックされていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="video_tdr_application_blocked-parameters"></a>VIDEO \_ TDR APPLICATION のブロックされた \_ \_ パラメーター


| パラメーター | 説明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 内部 TDR 復旧コンテキスト (TDR recovery context) へのポインター (省略可能 \_ \_ )。 |
| 2         | 責任を持つデバイスドライバーモジュール (所有者タグなど) へのポインター。          |
| 3         | セカンダリドライバー固有のバケットキー。                                |
| 4         | GPU へのアクセスがブロックされているプロセスの Id。                     |

 

<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに非常に役立ちます。
タグのセカンダリデータ {270a33fd3da647 60D-BA89-3c1bae21e39b} には、追加の TDR 関連データが含まれています。 [**Enumtag (セカンダリコールバックデータの列挙)**](-enumtag--enumerate-secondary-callback-data-.md)を使用してデータを表示します。
