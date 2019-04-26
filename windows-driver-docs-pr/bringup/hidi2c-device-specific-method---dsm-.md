---
title: HIDI2C のデバイス固有のメソッド (_DSM)
description: 9.14.1 で _DSM メソッドが定義されている \ 0034; _DSM (デバイスの特定のメソッド) \ 0034;、ACPI 5.0 仕様。
ms.assetid: D78077F4-9995-4DC6-9DF6-89D0F8E0C545
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f42a1f680caefbf0830a280346bd9953760bfd0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337607"
---
# <a name="hidi2c-device-specific-method-dsm"></a>HIDI2C デバイス固有のメソッド (\_DSM)


\_9.14.1 で DSM メソッドが定義されている"\_DSM (デバイスの特定のメソッド)"で、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。 このメソッドは、個々 のデバイス固有のデータとデバイス ドライバーなど他のデバイスに固有のメソッドで競合することがなく呼び出すことができるコントロール関数を提供します。

\_DSM は、特定のデバイスまたはクラスの定義、UUID (GUID) が、その他の Uuid と衝突しないように保証されています。 定義されている関数のセットがある各 UUID では、を\_のデータの提供やドライバーの制御関数を実行する DSM メソッドを実装できます。

HIDI2C クラスのデバイスでは、関数 1 は、次のように定義されます。

### <a name="arguments"></a>引数

-   **Arg0:** UUID 3cdff6f7-4267-4555-ad05-b30a3d8938de を =
-   **Arg1:** リビジョン ID = 1
-   **Arg2:** 関数インデックス = 1
-   **Arg3:** なし

### <a name="return"></a>戻り値

HidDescriptorAddress を含む整数。 このアドレスは、HID descriptor(s) を読み取ることができます、I2C デバイス内のオフセット レジスタです。
**注**  関数インデックス 0 の各\_DSM がサポートされている関数のインデックスのセットを返しますは常に必要とするクエリ関数を示します。 詳細については、セクション 9.14.1 を参照してください。"\_DSM (デバイスの特定のメソッド)"で、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

 

 

 




