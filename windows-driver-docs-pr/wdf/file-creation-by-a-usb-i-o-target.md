---
title: USB I/O ターゲットによるファイルの作成
description: USB I/O ターゲットによるファイルの作成
ms.assetid: 44bbc4c7-632d-4d75-94b9-f65e4d480e90
keywords:
- ユーザー モード ドライバー WDK UMDF、USB I/O ターゲットでは、ファイルの作成
- UMDF WDK、USB I/O ターゲット、ファイルの作成
- ユーザー モード ドライバー フレームワーク WDK、USB I/O ターゲット
- フレームワーク ベースのドライバー WDK UMDF、USB I/O ターゲット
- USB I/O ターゲット WDK UMDF、ファイルの作成
- I/O ターゲット WDK UMDF、USB、ファイルの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 868367ed25ef7b88ac0b7f8468a66c8fd848d7ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573564"
---
# <a name="file-creation-by-a-usb-io-target"></a>USB I/O ターゲットによるファイルの作成


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

初期化中には、USB I/O ターゲットは、USB I/O ターゲットを開いたまま既定のセッションを表す、スタック内のファイル オブジェクトを作成します。 スタック内のファイル オブジェクトの詳細については、次を参照してください。[ファイル I/O を処理するオブジェクトを作成する](creating-a-file-object-to-handle-i-o.md)します。 USB I/O ターゲットまたはその USB パイプ ターゲットの子は、このファイル オブジェクトを使用して、(たとえば、USB 構成記述子を取得する I/O など) が発生したすべての I/O を送信します。

ドライバーは、このスタック内のファイル オブジェクトを使用して、関数の形式 (などドライバーは、このファイル オブジェクトへのポインターを渡すことができます、 *pFile*への呼び出しでパラメーター、 [ **IWDFIoTarget:。FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)メソッド) 場合は、ドライバーは、このファイル オブジェクトの既定のセッションで I/O を送信する必要があります。 スタック内のファイル オブジェクトを取得するには、ドライバーを呼び出すことができます、 [ **IWDFIoTarget::GetTargetFile** ](https://msdn.microsoft.com/library/windows/hardware/ff559243)メソッド。

I/O ターゲットが破棄されるときのいずれか、明示的にドライバーを呼び出すときにスタック内のファイル オブジェクトが閉じて、 [ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)メソッド I/O ターゲット、または暗黙的に、ときに、/O ターゲットの親は破棄されます。

すべての I/O は、デバイスの削除時にこのスタック内のファイル オブジェクトの未処理残っている場合は、このファイル オブジェクトを閉じるには、失敗および UMDF ドライバーの停止が生成されます。 詳細については、次を参照してください。 [Using Driver-Created ファイル オブジェクトの作成と](creating-and-using-driver-created-file-objects.md)します。

 

 





