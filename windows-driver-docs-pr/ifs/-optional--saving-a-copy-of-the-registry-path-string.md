---
title: '[省略可能]レジストリのパス文字列のコピーを保存しています'
description: '[省略可能]レジストリのパス文字列のコピーを保存しています'
ms.assetid: cf3b8649-6fb0-4ada-816c-5c7783918b2f
keywords:
- RegistryPath 文字列のコピー
- RegistryPath 文字列のコピーを保存しています
- RegistryPath 文字列のコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eebf5f499a9342f46b4ce6e55ecb7c40b2371e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381765"
---
# <a name="optional-saving-a-copy-of-the-registry-path-string"></a>\[省略可能な\]レジストリのパス文字列のコピーを保存しています


## <span id="ddk_saving_a_copy_of_the_registry_path_string_if"></span><span id="DDK_SAVING_A_COPY_OF_THE_REGISTRY_PATH_STRING_IF"></span>


**注**  この手順は、フィルター ドライバーは、後にレジストリ パスを使用する必要がある場合にのみ、 **DriverEntry**ルーチンを返します。

 

コピーを保存、 *RegistryPath*への入力として渡された文字列を**DriverEntry**します。 このパラメーターが、ドライバーのレジストリ キーへのパスを指定する、カウントされた Unicode 文字列を指す **\\レジストリ\\マシン\\システム\\CurrentControlSet\\サービス\\** <em>DriverName</em>ここで、 *DriverName*ドライバーの名前を指定します。 場合、 *RegistryPath*文字列は、後で必要になります**DriverEntry**ポインターが後に無効になっているために、これだけでなく、ポインターのコピーを保存する必要があります、 **DriverEntry**ルーチンを返します。 使用することができます、 [ **RtlCopyUnicodeString** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcopyunicodestring)をコピーするルーチン、 *RegistryPath*を宛先文字列に文字列のソースします。

 

 




