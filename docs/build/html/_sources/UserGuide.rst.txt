.. Sample Writing documentation master file, created by
   sphinx-quickstart on Thu Jun  2 22:47:12 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Managing Platforms
===================

This section provides information about managing a platform using the ClearPath Forward
vSphere Plug-in user interface in the following topics:

- :ref:`Viewing the Platform Summary` 
- :ref:`Managing Power for Each Platform`
- :ref:`Viewing the Related Objects of a Platform`



.. _Viewing the Platform Summary:

Viewing the Platform Summary
----------------------------

To view a platform summary, perform the following:

   1. Expand the **Fabric** list, and click **Platforms.**

      The Platforms page appears with the platform details.
   2. Select the platform for which you want to view the summary.
   3. Click the **Summary** tab.

.. _Managing Power for Each Platform:

Managing Power for Each Platform
---------------------------------

You can perform various power operations, such as power-on, power-off, soft restart, and
soft shutdown on an enterprise platform in the ClearPath Forward fabric.

This section provides information about performing platform power operation in the
following topics:

- :ref:`Powering On a Platform`
- :ref:`Powering Off a Platform`
- :ref:`Performing Soft Restart on a Platform`
- :ref:`Performing Soft Shutdown on a Platform`

.. note::
   To monitor the operation click Recent Tasks, and then select All Users’ Tasks.


.. _Powering On a Platform:

Powering On a Platform
**********************

The powering on platform operation is equivalent to pressing the physical power switch.
This operation can only be performed if the platform is in a powered-off state. This option
is disabled if the platform is already powered on.

**Prerequisite:** The platform is powered off.

To power on a platform, perform the following steps:

   1. On the ClearPath Forward vSphere Plug-in user interface, go to the list of objects, and select the platform that you want to power on.

   2. From the **Actions** drop-down menu, click **Power ON.**

.. _Powering Off a Platform:

Powering Off a Platform
***********************

Powering off is an unorderly shutdown of the platform. This is equivalent to switching off
the computer by pressing the power button. The platform is turned off without an orderly
shutdown of its partition images and guest operating systems.

To power off a platform, perform the following steps:

   1. On the ClearPath Forward vSphere Plug-in user interface, go to the list of objects and select the platform that you want to power off.

   2. From the **Actions** drop-down menu, click **Power OFF.**


.. _Performing Soft Restart on a Platform:

Performing Soft Restart on a Platform
**************************************

Soft restart is to shutdown of the platform and partitions followed by a restart. Soft restart
is equivalent to clicking Start and then clicking the Shutdown and Restart options in a
computer running on the Windows operating system.

To soft restart a platform, perform the following steps:

   1. On the ClearPath Forward vSphere Plug-in user interface, go to the list of objects, and select the platform that you want to soft restart.

   2. From the **Actions** drop-down menu, click Soft **Restart.**


.. _Performing Soft Shutdown on a Platform:

Performing Soft Shutdown on a Platform
***************************************

The soft shutdown operation is an orderly shutdown of the platform, and is also known as
graceful shutdown. Soft shutdown is equivalent to clicking Start and then clicking the
Shutdown and Ok options in a computer running on the Windows operating system.
You can shutdown a platform, if it is in a powered-on state.

To soft shutdown a platform, perform the following steps:

   1. On the ClearPath Forward vSphere Plug-in user interface, go to the list of objects, and select the platform that you want to shutdown.

   2. From the **Actions** drop-down menu, click Soft **Shutdown.**


.. _Viewing the Related Objects of a Platform:

Viewing the Related Objects of a Platform
-------------------------------------------

To view the related objects of a platform, perform the following steps:

   1. Expand the **Fabric** list, and click **Platforms.**
   
      The Platforms page appears with the platform details.
   2. Select the platform for which you want to view the related objects.
   3. Click the **Related Objects** tab.

      A list of all the partitions is displayed with the following attributes:

         - **Partition Name:** Denotes the name of a related partition.
         - **Status:** Displays the status of the object.
         - **Health:** Displays the health of the object.
         - **Type:** Displays the type of the object.
         - **Platform Name:** Denotes the name of the platform on which the partition is commissioned.
         - **IP Address:** Displays the IP address of the object.
         - **Physical Ports:** Displays the physical ports of the partition.
         - **Logical Ports:** Displays the logical ports of the partition.

