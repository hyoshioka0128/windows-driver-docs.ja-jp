---
title: Windows で自動的に長いメッセージをセグメント化する
description: Windows で自動的に長いメッセージをセグメント化する
ms.assetid: 0c1d7347-4e53-4f17-bdb5-908479f903de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb156e8c27999f69ed367eb1ef3a625fe63cb1af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377295"
---
# <a name="windows-automatically-segments-long-messages"></a>Windows で自動的に長いメッセージをセグメント化する


モバイル ブロード バンド SMS プラットフォームは、メッセージの内容に基づいてサポートされている文字数の上限に収まる個別のセグメントに GSM ネットワークで送信される時間の長いメッセージを自動的にセグメントします。 セグメント化の情報 (つまり、2 の 1 の部分) で SMS ユーザー データのヘッダー (UDH)、1 つのメッセージにセグメントを結合する受信 SMS クライアントを有効にするのにはエンコードされます。 マルチパートの SMS のすべてのセグメントは、同じ文字セットを使用してエンコードされます。

モバイル ネットワーク オペレーターには、メッセージ セグメントあたりのユーザーが課金されます。 SMS プラットフォームは自動的に最大 10 個のセグメントを作成し、制限を超えてテキストが切り捨てられます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[テキスト モード インターフェイスを使用して SMS を送信します。](send-sms-by-using-the-text-mode-interface.md)

 

 






