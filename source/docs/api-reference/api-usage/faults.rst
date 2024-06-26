Device Faults
=============

"Faults" are status indicators on CTR Electronics CAN devices that indicate a certain behavior or event has occurred. Faults do not directly affect the behavior of a device; instead, they indicate the device's current status and highlight potential issues.

Faults are stored in two fashions. There are "live" faults, which are reported in real-time, and "sticky" faults, which assert persistently and stay asserted until they are manually cleared (like trouble codes in a vehicle).

Sticky Faults can be cleared by clicking the :guilabel:`Clear Faults` button in Phoenix Tuner X, or by calling ``clearStickyFaults()`` on the device in the robot program. A regular fault can only be cleared when the offending problem has been resolved.

.. image:: images/self-test-clear-faults.png
   :width: 70%
   :alt: Clear faults button in Tuner located in the top bar.

Using API to Retrieve Faults
----------------------------

Faults can also be retrieved in API using the ``getFault_*()`` (regular) or ``getStickyFault_*()`` (sticky) methods on the device object. This can be useful for diagnostics or error handling.

.. tab-set::

   .. tab-item:: Java
      :sync: java

      .. code-block:: java

         var faulted = m_cancoder.getFault_BadMagnet().getValue();

         if (faulted) {
            // do action when bad magnet fault is set
         }

   .. tab-item:: C++
      :sync: C++

      .. code-block:: cpp

         auto faulted = m_cancoder.GetFault_BadMagnet().GetValue();

         if (faulted) {
            // do action when bad magnet fault is set
         }

   .. tab-item:: Python
      :sync: python

      .. code-block:: python

         faulted = self.cancoder.get_fault_bad_magnet().value

         if faulted:
            # do action when bad magnet fault is set

A list of possible faults can be found in the API documentation for each device.

Using API to Clear Sticky Faults
--------------------------------

Sticky faults can be cleared in API using the ``clearStickyFaults()`` method on the device objects. Additionally, individual sticky faults may be cleared using the ``clearStickyFault_*()`` APIs.

.. note:: Clearing sticky faults is a blocking operation and should not be run in a periodic loop.

.. tab-set::

   .. tab-item:: Java
      :sync: java

      .. code-block:: java

         // clear the undervoltage sticky fault
         m_cancoder.clearStickyFault_Undervoltage();

   .. tab-item:: C++
      :sync: C++

      .. code-block:: cpp

         // clear the undervoltage sticky fault
         m_cancoder.ClearStickyFault_Undervoltage();

   .. tab-item:: Python
      :sync: python

      .. code-block:: python

         # clear the undervoltage sticky fault
         self.cancoder.clear_sticky_fault_undervoltage()
