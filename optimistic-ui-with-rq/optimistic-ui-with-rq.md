## INTRODUCTION

Here guys, in this short article, we are exploring how to create optismistic user experience with RTK Query. Optimistic updates is a user experience design pattern where updates to the server that have a high success rate are visually indicated as being successful while the updates happens in the background. Usually, this pattern is used where your backend service has a high availability and very minimal down time. Furthermore, mechanism for rolling back the visual indication is provided in the event the update fails. This is in contrast to permisssimitc updates where the user interface is only updated after the update queries to the server are successful.


## GETTING STARTED

This article assumes you are already familiar with RTK-Query and understands the benefits that libraries such as these are
