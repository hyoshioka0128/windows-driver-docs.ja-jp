---
title: デバイス オブジェクトのプロパティ
description: デバイス オブジェクトのプロパティ
ms.assetid: 6cd31263-e725-4a62-bec9-f40feb0b66cc
keywords:
- デバイス オブジェクトの WDK カーネル、プロパティ
- WDK のデバイス オブジェクトのプロパティ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d8078747a880457274da3b83c994770359567e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529264"
---
# <a name="properties-of-device-objects"></a>デバイス オブジェクトのプロパティ





各デバイス オブジェクトには、デバイスとデバイス オブジェクトが、システムと対話する方法について説明する特定のプロパティがあります。 デバイス オブジェクトのプロパティは次のとおりです。

-   デバイスの種類。 ハードウェアのデバイスの種類を指定します。 デバイスの種類の詳細については、[デバイスの種類の指定](specifying-device-types.md)を参照してください。

-   デバイスの特性。 デバイスに関する追加情報を指定するフラグを指定します。 詳細については、[デバイスの特性を指定する](specifying-device-characteristics.md)を参照してください。

-   排他アクセスします。 デバイス オブジェクトが表すかどうかを指定します、*排他デバイス*します。 デバイスが専用の場合は、ハンドルの 1 つだけ開くことができるデバイス オブジェクトを一度にします。 (基になるデバイスは、重複 I/O をサポートする場合は、同じプロセスの複数のスレッドは要求の単一のハンドルを送信できます)。詳細については、[デバイス オブジェクトに排他アクセスを指定する](specifying-exclusive-access-to-device-objects.md)を参照してください。

-   セキュリティ記述子。 デバイス オブジェクトのアクセスを制御するセキュリティ記述子があるデバイスにします。 詳細については、[デバイス オブジェクトのセキュリティで保護する](securing-device-objects.md)を参照してください。

これらのプロパティごとに、デバイス オブジェクトが作成されたときに、既定値を設定できます。 デバイス オブジェクトの作成方法の詳細については、[デバイス オブジェクトを作成する](creating-a-device-object.md)を参照してください。

デバイス オブジェクトのプロパティの値をレジストリの設定もできます。 参照してください[レジストリにデバイス オブジェクト プロパティの設定](setting-device-object-properties-in-the-registry.md)詳細についてはします。

 

 




