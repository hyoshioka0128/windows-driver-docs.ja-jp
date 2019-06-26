---
title: フィルターの初期化
description: フィルターの初期化
ms.assetid: c39dc5a6-f529-40a2-87d4-bac325b4fa1a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76db8b4f15d2ade619f941a84c67b547c7130db1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356010"
---
# <a name="filter-initialization"></a>フィルターの初期化


システムのクラッシュや休止状態のプロセスの初期段階でクラッシュ ダンプのドライバーが初期化されます。 ただし、フィルター ドライバーは読み込まれるとすぐに初期化されます。 これにより、フィルター ドライバーは、営業案件のクラッシュの初期化時のメモリの割り当てなどに行うことができないために必要な初期化を行います。

クラッシュ ダンプのドライバー スタックでは、フィルター ドライバーは、システムのブート時に初期化されます。 無効にし、再度有効にするクラッシュ ダンプ、いつでも、システムが実行されている場合、クラッシュ ダンプのフィルター ドライバーのドライバーの読み込みについて関知および時間をアンロードする必要がありますしないようにことができます。 休止状態のフィルター ドライバーは読み込まれ、休止状態の開始時に初期化します。

フィルター ドライバーがメモリに読み込まれた後、クラッシュ ダンプのドライバーは、フィルター ドライバーを初期化するために、フィルター ドライバーの DriverEntry 関数を呼び出します。 標準の DriverEntry 関数は、2 つの引数 (DriverObject および RegistryPath) を受け取ります。 DriverObject が指すフィルター ドライバーが呼び出されたときに、 [**フィルター\_拡張子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/ns-ntdddump-_filter_extension)構造、および RegistryPath を指して、 [**フィルター\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/ns-ntdddump-_filter_initialization_data)構造体。

初期化プロセスを完了する、フィルター ドライバーを初期化する必要があります、 [**フィルター\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/ns-ntdddump-_filter_initialization_data)構造体であり、クラッシュ ダンプのドライバーに戻すことができます。

 

 




