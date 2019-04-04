---
title: 取得して、VM キュー パラメーターの更新
description: 取得して、VM キュー パラメーターの更新
ms.assetid: 42beceec-95ae-48e3-985f-b6ee8a84d68b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd2785e9edb50c240fc0ee6f9a3a8b920eda919f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528780"
---
# <a name="obtaining-and-updating-vm-queue-parameters"></a>取得して、VM キュー パラメーターの更新





上にある、ドライバーに割り当てた後、VM のキューの構成パラメーターを設定できます。 また、上位のドライバーまたはアプリケーションはキューの現在のパラメーターと、キューに設定されているフィルターのパラメーターに取得できます。

キューの現在の構成パラメーターを変更するを使用してドライバーを重なってことができます、 [OID\_受信\_フィルター\_キュー\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569794) OID 要求のセット。 上にあるドライバーへのポインターを提供する、 [ **NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211)構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。

NDIS\_受信\_キュー\_パラメーター構造体がで使用される、 [OID\_受信\_フィルター\_ALLOCATE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569784) OID と[OID\_受信\_フィルター\_キュー\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569794) OID。 キューの割り当てに関する詳細については、[VM キューを割り当てる](allocating-a-vm-queue.md)を参照してください。

現在の構成を取得するキュー、ドライバーを後続のパラメーターが、OID を使用できます\_受信\_フィルター\_キュー\_パラメーター メソッド OID を要求します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_キュー\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567211) NDIS の種類のキューの id を使用した構造\_受信\_キュー\_Id。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**の NDIS メンバー\_OID\_要求の構造体にはへのポインターが含まれています、 **NDIS\_受信\_キュー\_パラメーター**構造体。

NDIS は、ミニポート ドライバー メソッド要求を処理します。 そのため、OID\_受信\_フィルター\_キュー\_メソッド OID 要求のパラメーターは、ミニポート ドライバーには要求されません。 NDIS OID から受信したデータの内部キャッシュから情報を入手した\_受信\_フィルター\_ALLOCATE\_キューと OID\_受信\_フィルター\_キュー\_パラメーターの OID を要求します。

現在の構成パラメーターを取得する受信キューでのフィルターを使用できますのドライバーが重なって、 [OID\_受信\_フィルター\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569792)メソッド要求の OID。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。 NDIS を使用して、 **FilterId**入力構造で、フィルターを特定のメンバー。 メソッドの要求から正常に戻った後、 **InformationBuffer**の NDIS メンバー\_OID\_構造には、更新された NDIS へのポインターが含まれる要求\_受信\_フィルター\_パラメーター構造体。

NDIS 処理 OID\_受信\_フィルター\_ミニポート ドライバーのパラメーター メソッド OID を要求します。 NDIS から受信したデータの内部キャッシュからの情報の取得、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795) OID 要求。

OID を使用できるドライバーが重なって\_受信\_フィルター\_パラメーター メソッド OID 要求受信キューでのフィルターの構成パラメーターを取得します。

上にあるドライバーは、以前の OID からフィルター id を取得した\_受信\_フィルター\_設定\_メソッド OID 要求のフィルターまたはから、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787) OID 要求。 ドライバーは、OID を使用できる専用\_受信\_フィルター\_設定\_フィルター要求。

アプリケーションからのフィルターの識別子を取得した、 [OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787) OID 要求。

 

 





