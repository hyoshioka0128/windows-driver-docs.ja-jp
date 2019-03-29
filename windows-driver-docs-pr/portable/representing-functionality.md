---
Description: Representing Functionality
title: 機能の表現
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca55b289195133a11db9a2e56c10f3442312de3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580240"
---
# <a name="representing-functionality"></a>機能の表現


機能のオブジェクトの目的を識別する、またはデバイスの機能を論理的にグループ化することです。 たとえば、アプリケーションでは、SMS 機能オブジェクトを探すことによって、デバイスがショート メッセージ サービス (SMS) をサポートしているを確認できます。 または、デバイスにイメージのキャプチャはまだ機能オブジェクトを探すことによってカメラ機能、アプリケーションが表示されます。

この柔軟性のあるオブジェクトの表現を使用すると、多機能の機能を使用したデバイスのサポート。 ドライバーは、どのような機能のオブジェクトが従来のデバイス クラスを使用してより細かいは各自のデバイスを表す公開できます。 重複する機能の部分を分離する便利です。 たとえば、一部の携帯電話には、2 つのカメラや、4 つの記憶装置があります。

Windows 7 以降では、サービス オブジェクトは、機能が豊富なクエリおよびコンテンツの抽象のグループ化を提供することで機能のオブジェクトを拡張します。 アプリケーションは、デバイスの機能を検出してより効率的にコンテンツと対話するサービス オブジェクトを使用できます。 たとえば、アプリケーションでは、デバイスが Microsoft 完全列挙同期連絡先サービスを実装するサービス オブジェクトを探すことによって、連絡先の同期をサポートしているを確認できます。 ここで、アプリケーションは、記憶域階層を検索することがなく、デバイス上のすべての連絡先を検索できます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





