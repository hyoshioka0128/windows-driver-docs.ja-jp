---
title: Windows が自動的に時間の長いメッセージをセグメントします。
description: Windows が自動的に時間の長いメッセージをセグメントします。
ms.assetid: 0c1d7347-4e53-4f17-bdb5-908479f903de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb156e8c27999f69ed367eb1ef3a625fe63cb1af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550206"
---
# <a name="windows-automatically-segments-long-messages"></a>Windows が自動的に時間の長いメッセージをセグメントします。


モバイル ブロード バンド SMS プラットフォームは、メッセージの内容に基づいてサポートされている文字数の上限に収まる個別のセグメントに GSM ネットワークで送信される時間の長いメッセージを自動的にセグメントします。 セグメント化の情報 (つまり、2 の 1 の部分) で SMS ユーザー データのヘッダー (UDH)、1 つのメッセージにセグメントを結合する受信 SMS クライアントを有効にするのにはエンコードされます。 マルチパートの SMS のすべてのセグメントは、同じ文字セットを使用してエンコードされます。

モバイル ネットワーク オペレーターには、メッセージ セグメントあたりのユーザーが課金されます。 SMS プラットフォームは自動的に最大 10 個のセグメントを作成し、制限を超えてテキストが切り捨てられます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[テキスト モード インターフェイスを使用して SMS を送信します。](send-sms-by-using-the-text-mode-interface.md)

 

 






