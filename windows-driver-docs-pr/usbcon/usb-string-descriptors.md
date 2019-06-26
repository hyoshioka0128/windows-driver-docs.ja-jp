---
Description: デバイス、構成、およびインターフェイスの記述子には、文字列記述子への参照を含めることができます。 このトピックでは、デバイスから特定の文字列記述子を取得する方法について説明します。
title: USB 文字列記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5aeaa3da6840742a2a76d057992c60a74a0039e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356568"
---
# <a name="usb-string-descriptors"></a>USB 文字列記述子


デバイス、構成、およびインターフェイスの記述子には、文字列記述子への参照を含めることができます。 このトピックでは、デバイスから特定の文字列記述子を取得する方法について説明します。




文字列記述子は、1 から始まるインデックス番号で参照されます。 文字列記述子には、1 つ以上の Unicode 文字列; が含まれています。各文字列は、他の他の言語に翻訳します。

クライアント ドライバーを使用して、 [ **UsbBuildGetDescriptorRequest**](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))で*DescriptorType* = USB\_文字列\_記述子\_型を文字列記述子を取得する要求を構築します。 *インデックス*パラメーターは、インデックス番号を指定し、 *LanguageID*パラメーター (Microsoft Win32 LANGID 値と同じ値が使用されます)、言語 ID を指定します。 ドライバーは、デバイスをサポートしている言語 Id にゼロの特殊なインデックス番号を要求できます。 この特別な値は、デバイスは、Unicode 文字列ではなく、言語 Id の配列を返します。

文字列記述子が可変長のデータで構成されているため、ドライバーする必要がありますで取得する 2 つの手順。 ドライバーが要求は、USB、文字列記述子のヘッダーを保持するために十分な大きさのデータ バッファーを渡すことを発行する必要がありますまず\_文字列\_記述子構造体。 **BLength** USB のメンバー\_文字列\_記述子記述子全体のバイト単位のサイズを指定します。 ドライバーはサイズのデータ バッファーと共に同じ要求し、 **bLength**します。

次のコードを要求する方法を示して、*は*番目文字列記述子では、言語 ID を持つ*langID*:

```cpp
USB_STRING_DESCRIPTOR USD, *pFullUSD;
UsbBuildGetDescriptorRequest(
    pURB, // points to the URB to be filled in
    sizeof(struct _URB_CONTROL_DESCRIPTOR_REQUEST),
    USB_STRING_DESCRIPTOR_TYPE,
    i, // index of string descriptor
    langID, // language ID of string.
    &USD, // points to a USB_STRING_DESCRIPTOR.
    NULL,
    sizeof(USB_STRING_DESCRIPTOR),
    NULL
);
pFullUSD = ExAllocatePool(NonPagedPool, USD.bLength);
UsbBuildGetDescriptorRequest(
    pURB, // points to the URB to be filled in
    sizeof(struct _URB_CONTROL_DESCRIPTOR_REQUEST),
    USB_STRING_DESCRIPTOR_TYPE,
    i, // index of string descriptor
    langID, // language ID of string
    pFullUSD,
    NULL,
    USD.bLength,
    NULL
);
```

## <a name="related-topics"></a>関連トピック
[USB ディスクリプター](usb-descriptors.md)  



