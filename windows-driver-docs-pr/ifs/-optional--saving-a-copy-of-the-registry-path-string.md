---
title: Optionalレジストリパス文字列のコピーを保存しています
description: Optionalレジストリパス文字列のコピーを保存しています
ms.assetid: cf3b8649-6fb0-4ada-816c-5c7783918b2f
keywords:
- RegistryPath 文字列のコピー
- RegistryPath 文字列のコピーを保存しています
- RegistryPath 文字列のコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 890dfcfa26e341939dad8b60e7796c93264f2762
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841516"
---
# <a name="optional-saving-a-copy-of-the-registry-path-string"></a>\[オプション\] レジストリパス文字列のコピーを保存します。


## <span id="ddk_saving_a_copy_of_the_registry_path_string_if"></span><span id="DDK_SAVING_A_COPY_OF_THE_REGISTRY_PATH_STRING_IF"></span>


**注**   この手順が必要なのは、 **driverentry**ルーチンから制御が戻った後にフィルタードライバーがレジストリパスを使用する必要がある場合のみです。

 

入力として**Driverentry**に渡された*RegistryPath*文字列のコピーを保存します。 このパラメーターは、ドライバーのレジストリキーへのパスを指定する、カウントされた Unicode 文字列を指しています。 **\\レジストリ\\マシン\\System\\CurrentControlSet\\Services\\** *ドライバー名ドライバー名を指定*します。 後で*RegistryPath*文字列が必要になった場合、driverentry**は driverentry ルーチンが**返された後にポインターが無効になるため、 **driverentry**はポインターだけではなく、そのコピーを保存する必要があります。 [**RtlCopyUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcopyunicodestring)ルーチンを使用して、 *RegistryPath*ソース文字列をコピー先の文字列にコピーできます。

 

 




