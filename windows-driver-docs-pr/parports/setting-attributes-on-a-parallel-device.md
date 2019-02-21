---
title: 並列のデバイスに属性を設定
description: 並列のデバイスに属性を設定
ms.assetid: 10df9a1b-99ec-46b1-b515-10fb20fe2aed
keywords:
- デバイスの属性、WDK を並列します。
- デバイスの並列属性 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b0d430a405c113f99b0ad4c307e88464ef490da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529077"
---
# <a name="setting-attributes-on-a-parallel-device"></a>並列のデバイスに属性を設定





並列のデバイスの指定された操作を設定する次のデバイスに対する制御要求クライアントを使用します。

-   [**IOCTL\_PAR\_設定\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544103)並列デバイスを初期化します。

-   [**IOCTL\_シリアル\_設定\_タイムアウト**](https://msdn.microsoft.com/library/windows/hardware/ff544126)並列デバイス用のタイムアウトを設定します。

-   [**IOCTL\_PAR\_設定\_読み取り\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff544107) ECP または並列デバイス アドレス (チャネル) を読み取る EPP を設定します。

-   [**IOCTL\_PAR\_設定\_書き込み\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/ff544115) ECP または EPP 書き込み (チャネル) のアドレス、並列のデバイスを設定します。

 

 




