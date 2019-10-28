---
title: CPSUI オプションの種類
description: CPSUI オプションの種類
ms.assetid: 3b3c002c-a201-4f81-b208-30864343409b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bd038401eb28da4d08094a230edda8ad8aadbe9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843063"
---
# <a name="cpsui-option-types"></a>CPSUI オプションの種類


## <span id="ddk_cpsui_option_types_gg"></span><span id="DDK_CPSUI_OPTION_TYPES_GG"></span>


CPSUI を使用してプロパティシートページを作成する場合、ユーザーが選択できるオプションは、 [CPSUI でサポートされているウィンドウコントロール](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-supported-window-controls)を使用して定義する必要があります。 これらのコントロールは、次の CPSUI オプションの種類によって識別されます。

[**TVOT\_2STATES**](tvot-2states.md)

[**TVOT\_3STATES**](tvot-3states.md)

[**TVOT\_CHKBOX**](tvot-chkbox.md)

[**TVOT\_COMBOBOX**](tvot-combobox.md)

[**TVOT\_エディットボックス**](tvot-editbox.md)

[**TVOT\_LISTBOX**](tvot-listbox.md)

[**TVOT\_プッシュボタン**](tvot-pushbutton.md)

[**TVOT\_SCROLLBAR**](tvot-scrollbar.md)

[**TVOT\_TRACKBAR**](tvot-trackbar.md)

[**TVOT\_UDARROW**](tvot-udarrow.md)

オプションの型は、 [**opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)構造体の**型**メンバーで指定されています。

 

 




