---
title: 文字列オブジェクトの使用
description: このトピックでは、Windows Driver Framework (WDF) が文字列オブジェクトに対して提供するサポートについて説明します。 これは、カーネルモードドライバーフレームワーク (KMDF) の両方に適用されます。
ms.assetid: b1d52a18-ebd5-4ba7-b5c7-3ef3d298c82e
keywords:
- 文字列オブジェクト WDK KMDF
- framework オブジェクト WDK KMDF、string オブジェクト
- Unicode 文字列 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7be4d5f23261f44ca2abb04272355093f1e832a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845425"
---
# <a name="using-string-objects"></a>文字列オブジェクトの使用


このトピックでは、Windows Driver Framework (WDF) が文字列オブジェクトに対して提供するサポートについて説明します。 これは、バージョン2以降のカーネルモードドライバーフレームワーク (KMDF) ドライバーとユーザーモードドライバーフレームワーク (UMDF) ドライバーの両方に適用されます。




WDF は Unicode 文字列のみを使用します。 Framework オブジェクトによって定義されるすべてのメソッドは、Unicode 文字列のみを受け入れます。

このフレームワークは、KMDF および UMDF ドライバーが Unicode 文字列を表すために使用できる*フレームワーク文字列オブジェクト*を定義します。

ドライバーは、 [**Wdfstringcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringcreate)を呼び出して文字列オブジェクトを作成し、必要に応じて Unicode 文字列をオブジェクトに割り当てることができます。

[**Wdfregistryquerystring**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerystring)など、フレームワークのオブジェクトメソッドの中には、文字列オブジェクトハンドルを入力として受け取り、文字列オブジェクトに文字列を割り当てるものがあります。

文字列オブジェクトに割り当てられている文字列にアクセスするために、ドライバーは[**WdfStringGetUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringgetunicodestring)を呼び出すことができます。

 

 





