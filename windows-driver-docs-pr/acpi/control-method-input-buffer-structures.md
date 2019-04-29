---
title: 制御メソッドの入力バッファーの構造
description: 制御メソッドの入力バッファーの構造
ms.assetid: 41d4c53f-9dc7-4723-9707-ae48ff07f5f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ee217a998db52c4bdc6c81c05ca9fc42c1d65e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328840"
---
# <a name="control-method-input-buffer-structures"></a>制御メソッドの入力バッファーの構造


ACPI のドライバーでは、 [ **IOCTL\_ACPI\_EVAL\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff536148)要求。 デバイスのドライバーは、この要求を使用して、要求を送信するデバイスの ACPI 名前空間で直接の子オブジェクトであるコントロールのメソッドを評価することができます。 IOCTL\_ACPI\_EVAL\_メソッド要求は、次の入力の構造をサポートします。

<a href="" id="acpi-eval-input-buffer"></a>[**ACPI\_EVAL\_入力\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff536115)  
この構造体は、バッファーの署名と、入力引数を受け取らないコントロール メソッドの名前を提供します。

<a href="" id="acpi-eval-input-buffer-simple-integer"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純\_整数**](https://msdn.microsoft.com/library/windows/hardware/ff536119)  
この構造体は、構造体の署名、コントロールのメソッドの名前と ULONG 型の 1 つの入力引数の値を提供します。

<a href="" id="acpi-eval-input-buffer-simple-string"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff536121)  
この構造体は、構造体の署名、コントロールのメソッドでは、および NULL で終わる ASCII 文字列である入力引数の名前を指定します。

<a href="" id="acpi-eval-input-buffer-complex"></a>[**ACPI\_EVAL\_入力\_バッファー\_複雑な**](https://msdn.microsoft.com/library/windows/hardware/ff536116)  
この構造体、構造体の署名、コントロールのメソッドの名前の入力配列を提供する[ **ACPI\_メソッド\_引数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)構造体。 配列は、このような 7 つの構造体の最大数を含めることができます。 ACPI\_メソッド\_引数が構造体は、ULONG 整数、ASCII 文字列、ACPI パッケージの説明、またはカスタム データの配列に含めることができます。

Windows にもサポートしています、 [ **IOCTL\_ACPI\_EVAL\_メソッド\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff536149)要求。 デバイスのドライバーは、この要求を使用して、要求を送信するデバイスの ACPI 名前空間内の子オブジェクトであるコントロールのメソッドを評価することができます。 IOCTL\_ACPI\_EVAL\_メソッド\_要求例には、次の入力の構造をサポートします。

<a href="" id="acpi-eval-input-buffer-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_例**](https://msdn.microsoft.com/library/windows/hardware/ff536118)  
この構造体の構造とパスと名前を入力引数を受け取らないコントロール メソッドのシグネチャを提供します。

<a href="" id="acpi-eval-input-buffer-simple-integer-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純\_整数\_例**](https://msdn.microsoft.com/library/windows/hardware/ff536120)  
この構造体の構造とパスと名前を入力引数として型 ULONG64 の 1 つの整数を受け取る control メソッドのシグネチャを提供します。

<a href="" id="acpi-eval-input-buffer-simple-string-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純\_文字列\_例**](https://msdn.microsoft.com/library/windows/hardware/ff536122)  
この構造体の構造とパスと名前を入力引数として 1 つの NULL で終わる ASCII 文字列を受け取る control メソッドのシグネチャを提供します。

<a href="" id="acpi-eval-input-buffer-complex-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_複雑な\_例**](https://msdn.microsoft.com/library/windows/hardware/ff536117)  
この構造体、構造、および、パスと ACPI の配列を受け取る control メソッドの名前の署名を提供する\_メソッド\_引数が入力として構造体します。 配列は、このような 7 つの構造体の最大数を含めることができます。 ACPI\_メソッド\_引数が構造体は、ULONG 整数、ASCII 文字列、ACPI パッケージの説明、またはカスタム データの配列に含めることができます。

デバイスのドライバーの使用のデバイスを ACPI 名前空間内の子オブジェクトの名前とパスを取得することができます、 [ **IOCTL\_ACPI\_ENUM\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536147)要求として説明されている[列挙子のデバイスとコントロール メソッド](enumerating-child-devices-and-control-methods.md)します。
