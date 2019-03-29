---
title: VMQ のフィルターの列挙
description: VMQ のフィルターの列挙
ms.assetid: 6d5d8cb6-7bdf-488b-8fcd-7c6e78c4fb24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d8224e35ab0430119228e0b90fa5c0fa27cc3ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578440"
---
# <a name="enumerating-filters-on-a-vmq"></a>VMQ のフィルターの列挙





受信キューに設定されているすべてのフィルターの一覧を取得する関連ドライバーおよびアプリケーション使用できます、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)メソッド オブジェクト識別子 (OID) 要求します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)構造体。 書式設定すると、 **NDIS\_受信\_フィルター\_情報\_配列**構造、上にあるドライバーまたはアプリケーションを設定する必要があります、 **QueueId**受信キューの識別子 (ID) のメンバー。 次の方法で受信キューの ID を取得します。

-   上にあるドライバーを以前の OID メソッド要求の受信キューの ID 値を取得した[OID\_受信\_フィルター\_ALLOCATE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569784)または[OID\_受信\_フィルター\_ENUM\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569788)します。 ドライバーを指定できますも**NDIS\_既定\_受信\_キュー\_ID**既定のキューを受信します。

-   アプリケーションの以前の OID メソッド要求から受信したキューの ID 値を取得した[OID\_受信\_フィルター\_ENUM\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569788)します。 アプリケーションを指定できますも**NDIS\_既定\_受信\_キュー\_ID**既定のキューを受信します。

OID メソッド要求から正常に戻った後[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造には、更新されたへのポインターが含まれる[ **NDIS\_受信\_フィルター\_情報\_配列**](https://msdn.microsoft.com/library/windows/hardware/ff567179)構造体が 1 つまたは複数続く[ **NDIS\_受信\_フィルター\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff567176)構造体。 各**NDIS\_受信\_フィルター\_情報**構造体を指定された受信キューが設定されているフィルターの ID を指定します。

使用できるドライバーやアプリケーションが重なって、 [OID\_受信\_フィルター\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569792) OID メソッド要求の受信キューで特定のフィルターのパラメーターを取得します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。 上にあるドライバーまたはアプリケーションの形式、 **NDIS\_受信\_フィルター\_パラメーター**構造体を設定して、 **FilterId**メンバーを 0 以外の IDパラメーターが返されるフィルターの値。

**注**  上にあるドライバーの以前の OID メソッド要求から、フィルター ID を取得した[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)または[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)します。 アプリケーションは、OID の以前の OID メソッド要求からのみ、フィルター ID を取得できます\_受信\_フィルター\_ENUM\_フィルター。

 

NDIS ハンドル、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)と[OID\_受信\_フィルター\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569792)メソッド OID は、ミニポート ドライバーを要求します。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795) OID 要求。

 

 





