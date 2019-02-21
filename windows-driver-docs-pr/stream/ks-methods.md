---
title: KS メソッド
description: KS メソッド
ms.assetid: 1d7bd6f4-0aaf-4d77-8132-f551fd2ecbd2
keywords:
- カーネルの WDK、メソッドのストリーミング
- KS WDK、メソッド
- ストリーミング メソッド WDK カーネル
- メソッドは、WDK のストリームを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbfd0f7b38e0282710a812d60661b7532b1aebbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548591"
---
# <a name="ks-methods"></a>KS メソッド





メソッドのセットは、ストリーミング クライアントのカーネルは、KS オブジェクトで呼び出すことができる関連するアクションのグループです。 たとえば、アロケーター オブジェクトには、設定の割り当てし、メモリの割り当てを解除するメソッドを格納しているメソッドを提供できます。

ミニドライバーの提供、 [ **KSMETHOD\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff563423)サポートする各メソッド設定の構造体します。 さらに、KSMETHOD\_セット構造体には配列が含まれています[ **KSMETHOD\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563420) 1 つのメソッドを記述する構造体。 ドライバーによって提供されるへのポインターを提供する、ミニドライバー [ *KStrMethodHandler* ](https://msdn.microsoft.com/library/windows/hardware/ff567191)と[ *KStrSupportHandler* ](https://msdn.microsoft.com/library/windows/hardware/ff567206)処理ルーチンで**MethodHandler**と**SupportHandler** 、KSMETHOD のメンバー\_項目の構造体。

クライアントが呼び出すことによって同期メソッドの要求を行う[ **KsSynchronousDeviceControl**](https://msdn.microsoft.com/library/windows/hardware/ff567142)、または呼び出すことによって、非同期要求**DeviceIoControl** (で説明されている、Microsoft Windows SDK のドキュメント) で[ **IOCTL\_KS\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff560817)します。

ドライバーが提供することで、特定のメソッドを要求する[ **KSMETHOD** ](https://msdn.microsoft.com/library/windows/hardware/ff563398)構造体、 *InBuffer*上の呼び出しのパラメーター。

AVStream フィルターとピンが提供することによってサポートされる方法を説明します、 [ **KSAUTOMATION\_テーブル**](https://msdn.microsoft.com/library/windows/hardware/ff560990)構造体、 **AutomationTable**のメンバーいずれかを[ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)構造または[ **KSPIN\_記述子\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。 詳細については、次を参照してください。 [Automation テーブルを定義する](defining-automation-tables.md)します。

 

 




