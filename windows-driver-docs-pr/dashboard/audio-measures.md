---
title: オーディオの測定値
description: オーディオの測定値では、オーディオ ドライバーのフライティング時に、良性の初期化エラーがフィルターで除外されます
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 79e13ea531c50935902b0724d105bb3575506250
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017091"
---
# <a name="audio-measures"></a>オーディオの測定値

## <a name="description"></a>説明

Windows Core Audio API では、オーディオを再生またはキャプチャするオーディオ デバイスとアプリケーションとの間の接続を表す概念として**ストリーム**を導入しています。ここでは、1 つのアプリケーションに複数のオーディオ ストリームが存在する場合があります。 アプリケーションで初期化されるすべてのストリームは**セッション**に割り当てられます。これによって、割り当てられた各ストリームの入力と出力が管理されます。 アプリケーションは Windows Core Audio API を呼び出すことができます。それが、初期化が成功したかどうかを示す成功または失敗のコードを返します。 これらの失敗コードは、エンドポイントがもう存在しない場合のように無視してかまわないこともあれば、バグが発生した後に初期化が失敗したという深刻な場合もあります。

オーディオの測定値では、良性の初期化エラーがフィルターで除外されます。これらのエラーの一覧については、[付録](/measure-appendix.md)をご覧ください。
