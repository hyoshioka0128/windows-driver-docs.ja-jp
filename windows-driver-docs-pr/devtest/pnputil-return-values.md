---
title: PnPUtil 戻り値します。
description: PnPUtil 戻り値します。
ms.assetid: c26ecf54-b3d4-4559-9ec1-ff535cf03d77
ms.date: 02/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0cdc4b82841cc2726edc438e548afc3feb5d27cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537972"
---
# <a name="pnputil-return-values"></a>PnPUtil 戻り値します。


次の表には、PnPUtil ツールによって返される一般的な値の一部が含まれます。

* `ERROR_SUCCESS` (0):要求された操作が正常に完了しました。
* `ERROR_SUCCESS_REBOOT_REQUIRED` (3010):要求された操作を正常に完了し、システムの再起動が必要です。  たとえば場合、`/install /add-driver`オプションが指定されて、1 つまたは複数のデバイスは正常にインストールおよびインストールを完了する、システムの再起動が必要です。
* `ERROR_SUCCESS_REBOOT_INITIATED` (1641):操作が成功し、ために、システムの再起動が進行中、`/reboot`オプションが指定されました。

Pnputil ツールを使用して、一括ドライバーをインストールすることができますが、実用的な戻り値を取得するをお勧め指定`/install /add-driver`一度に 1 つの INF にします。
