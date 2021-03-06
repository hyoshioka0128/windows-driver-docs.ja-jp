---
title: BDA ミニドライバーの脅威の防止
description: BDA ミニドライバーの脅威の防止
ms.assetid: 090cd2fb-d35b-4c42-a90d-a0d567d4b93f
keywords:
- ドライバーのアーキテクチャの WDK AVStream、セキュリティをブロードキャストします。
- BDA WDK AVStream、セキュリティ
- セキュリティ WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7db8f493fbf0adf49442bb6d013a5436940aebfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379078"
---
# <a name="preventing-bda-minidriver-threats"></a>BDA ミニドライバーの脅威の防止





可能性のある脅威[BDA ミニドライバーに導入された](introducing-threats-to-a-bda-minidriver.md)次の方法で防ぐことができます。

<a href="" id="threats-in-the-signal-transport-stream"></a>シグナルのトランスポート ストリームでの脅威  
BDA ミニドライバーがシグナルのペイロードの内容を解釈する必要がありますので、このような内容が破壊される可能性があります。 BDA ミニドライバーは、ペイロードのバッファーをアセンブルし、次のフィルターに渡すことのみ必要があります。

 

BDA ミニドライバーは、ペイロードを読み取る場合、ペイロードからこのような内容を解析するときに内容を慎重に確認する必要があります。

<a href="" id="threats-from-special-purpose-ioctls"></a>特殊な用途の Ioctl からの脅威  
BDA ミニドライバーは、バス、メモリ、または他のハードウェアを直接制御するようにアプリケーションを許可するアプリケーションへのインターフェイスを公開しないでください。 そのため、すべての特殊な用途 Ioctl の処理は、BDA ミニドライバーから削除する必要があります。 このような Ioctl には、たとえば、デバッグ Ioctl ベンダーが作成したにはが含まれます。 BDA ミニドライバーの実装は、このような Ioctl を処理する、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)ルーチンをディスパッチします。

<a href="" id="threats-from-direct-wdm-dispatch-routines"></a>脅威直接 WDM からディスパッチ ルーチン  
BDA ミニドライバーは、カーネルのストリーミング (KS) クラスのモデルをバイパスする WDM ディスパッチ ルーチンを提供しない必要があります。 BDA ミニドライバーは、提供する、KS ドライバーの AVStream モジュールを使用する必要があります[ディスパッチ](creating-dispatch-tables.md)と[automation](defining-automation-tables.md)ルーチンのため、セキュリティ チェックも用意されています。 直接 WDM ディスパッチ ルーチンを提供する BDA ミニドライバーは実装のいずれか、 [IRP の主な機能コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)します。

 

 




