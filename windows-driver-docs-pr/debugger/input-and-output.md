---
title: 入力と出力
description: 入力と出力
ms.assetid: 78e181c1-c577-49ca-910b-d2e8db2495b5
keywords:
- デバッガー エンジン、入力し、出力
- 入力と出力
- 出力
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b468aedee74ed0f07e5127eff8fd6bf16ae86a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572051"
---
# <a name="input-and-output"></a>入力と出力


入力と出力の機能、[デバッガー エンジン](introduction.md#debugger-engine)対話型デバッガー操作とログ記録に使用できます。 入力は、コマンドと、ユーザーによって入力された応答に通常表し、出力は、通常、ユーザーに表示される、またはログ ファイルに送信される情報を表します。

デバッガー エンジンは、保持、*入力ストリーム*と*出力ストリーム*します。 入力ストリームと出力ストリームに送信される出力から入力を要求できます。

ときに、 [**入力**](https://msdn.microsoft.com/library/windows/hardware/ff550962)メソッドを呼び出して、エンジンの入力ストリームからの入力を要求する、エンジンがすべて呼び出し、登録済み[コールバックを入力](using-input-and-output.md#input-callbacks)であることを通知するには入力を待機しています。 入力のコールバックを呼び出すことによって、入力を提供し、待機、 [ **ReturnInput** ](https://msdn.microsoft.com/library/windows/hardware/ff554600)メソッド。

エンジンが登録されている呼び出しをエンジンの出力ストリームに出力が送信されると、[コールバックを出力](using-input-and-output.md#output-callbacks)に出力を渡します。 出力ストリームに出力を送信するときに、クライアント オブジェクトでフィルタできます。この場合は、特定のクライアント オブジェクトに登録されている出力コールバックのみ、出力が返されます。

入力と出力ストリームは、リモート クライアントに透過的に使用できます。 リモート クライアントの入力を要求でき、エンジンの入力と出力ストリームに出力を送信し、エンジンは入力を要求または出力を送信するリモート クライアントに登録されているコールバックを呼び出します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

入力と出力の使用に関する詳細については、[を使用して入力と出力](using-input-and-output.md)を参照してください。 詳細および入力と出力のコールバック クライアント オブジェクトについては、[クライアント オブジェクト](client-objects.md)を参照してください。

 

 





