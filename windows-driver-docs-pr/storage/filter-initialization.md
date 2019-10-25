---
title: フィルターの初期化
description: フィルターの初期化
ms.assetid: c39dc5a6-f529-40a2-87d4-bac325b4fa1a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98d0a0f7cc53e3ba731bf9c9ea1e0c55e019809b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837969"
---
# <a name="filter-initialization"></a>フィルターの初期化


クラッシュダンプドライバーは、システムクラッシュまたは休止状態のプロセスの初期段階で初期化されます。 ただし、フィルタードライバーは、読み込まれるとすぐに初期化されます。 これにより、フィルタードライバーは、メモリの割り当てなど、クラッシュの初期化時には実行できない必要な初期化を実行できるようになります。

クラッシュダンプドライバースタックでは、フィルタードライバーはシステムの起動時に初期化されます。 システムが実行されているときはいつでもクラッシュダンプを無効にして再度有効にすることができます。そのため、クラッシュダンプフィルタードライバーは、ドライバーの読み込みとアンロードの時間について想定しているわけではありません。 休止状態の場合、休止状態が開始されると、フィルタードライバーが読み込まれ、初期化されます。

フィルタードライバーがメモリに読み込まれると、クラッシュダンプドライバーはフィルタードライバーの DriverEntry 関数を呼び出してフィルタードライバーを初期化します。 標準 DriverEntry 関数は、2つの引数 (Driverentry と RegistryPath) を受け取ります。 フィルタードライバーが呼び出されると、DriverObject は[**フィルター\_拡張**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/ns-ntdddump-_filter_extension)構造体をポイントし、RegistryPath はフィルター [ **\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/ns-ntdddump-_filter_initialization_data)構造をポイントします。

初期化プロセスを完了するには、フィルタードライバーによって[**フィルター\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdddump/ns-ntdddump-_filter_initialization_data)構造が初期化され、クラッシュダンプドライバーに返されます。

 

 




