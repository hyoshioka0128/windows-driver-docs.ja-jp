---
title: Property-Data-Type 識別子
description: Property-Data-Type 識別子
ms.assetid: 8deb96d8-c18c-48f2-be5d-1a3fc8ba8508
keywords:
- デバイスの WDK デバイス インストールでは、データ型のプロパティの識別子のプロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef4e2da61affe00817048d5a336821d27d2afec3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380474"
---
# <a name="property-data-type-identifiers"></a>Property-Data-Type 識別子


データ型のプロパティの識別子が、 [ **DEVPROPTYPE**](https://docs.microsoft.com/previous-versions/ff543546(v=vs.85))-プロパティのデータ形式を表す値を入力します。 一般に、データ型のプロパティの識別子は、のビットごとの OR、 [**基本データ型識別子**](https://docs.microsoft.com/previous-versions/ff537793(v=vs.85))と[**プロパティ データ型の修飾子**](https://docs.microsoft.com/previous-versions/ff549770(v=vs.85)). データ型のプロパティの識別子には、1 つの固定長データ型のベース値、1 つの可変長データ型のベース値、固定長基本データ型の値の配列または可変長の基本データ型の値の一覧を表すことができます。

システムでサポートされている基本データ型識別子と修飾子のデータ型のプロパティで定義されます*Devpropdef.h*します。

Windows では、データ型のプロパティの識別子では、次の要件を適用します。

-   基本データ型識別子は、いずれか、DEVPROP_TYPE_*Xxx*識別子。

-   基本データ型識別子がある場合[ **DEVPROP_TYPE_EMPTY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-empty)または[ **DEVPROP_TYPE_NULL**](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-null)プロパティのデータ型識別子データ型のプロパティの修飾子を含めることはできません。

-   プロパティ データ型修飾子は、DEVPROP_TYPEMOD_ のいずれかのデータ型のプロパティの識別子には、データ型のプロパティの修飾子が含まれている場合*Xxx*識別子。

-   [ **DEVPROP_TYPEMOD_ARRAY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-typemod-array)プロパティ データ型の修飾子を固定長の基本データ型とのみ組み合わせることができます。

-   [ **DEVPROP_TYPEMOD_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-typemod-list)プロパティ データ型の修飾子は可変長の基本データ型とのみ組み合わせることができます。

Windows プロパティのデータ型識別子の要件を適用するだけでなく適用も[プロパティ値要件](property-value-requirements.md)プロパティのデータ型に依存します。

SetupAPI プロパティ関数を取得し、プロパティを設定する値を*PropertyType*パラメーター。 プロパティの値を取得する関数を*PropertyType*プロパティのデータ型のプロパティの識別子を受け取る出力パラメーターです。 プロパティ値を設定する関数を*PropertyType*デバイス プロパティのデータ型のプロパティの識別子を提供する入力パラメーターです。

詳細については、次を参照してください。[プロパティにアクセスするデバイス (Windows Vista 以降) を使用して SetupAPI](using-setupapi-to-access-device-properties--windows-vista-and-later-.md)します。

 

 





