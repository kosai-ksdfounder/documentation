==================
Removal strategies
==================

For companies with warehouses, *removal strategies* determine **which** products are taken from the
warehouse, and **when**. For example, for perishable products, prioritizing those with the closest
expiration date is crucial to minimizing spoilage.

Leverage removal strategies to have Odoo automatically select how products are selected for orders.

The following are the removal strategies available in Odoo, detailing how the pickings are
determined, and the picking order:

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * -
     - :ref:`FIFO <inventory/removal/fifo>`
     - :ref:`LIFO <inventory/removal/lifo>`
     - :ref:`FEFO <inventory/removal/fefo>`
     - :ref:`Closest Location <inventory/removal/close>`
     - :ref:`Least Packages <inventory/removal/package>`
   * - Default
     - Yes
     - No
     - No
     - No
     - No
   * - Based on
     - :ref:`Incoming date <inventory/removal/arrival_date>`
     - :ref:`Incoming date <inventory/removal/arrival_date>`
     - :ref:`Removal date <inventory/removal/removal-date>`
     - :ref:`Location sequence <inventory/removal/sequence>`
     - Package's contained Quantity
   * - Selection order
     - First in
     - Last in
     - First to expire
     - Alphanumeric name of location
     - Quantity closest to fulfilling demand

.. _inventory/routes/strategies/set:

Configuration
=============

Removal strategies are set on either the product category or storage location.

Configure removal strategies on the location by going to :menuselection:`Inventory --> Configuration
--> Locations`, and select the desired location. On the location form, choose a removal
strategy from the :guilabel:`Removal Strategy` field's drop-down menu options.

.. important::
   To set a removal strategy on a location, the :guilabel:`Storage Locations` and
   :guilabel:`Multi-Step Routes` settings **must** be enabled in :menuselection:`Inventory -->
   Configuration --> Settings`.

   These features are **only** necessary when setting the removal strategy on a location.

Configure removal strategies on product categories by going to :menuselection:`Inventory -->
Configuration --> Product Categories` and selecting the intended product category. Next, choose the
:guilabel:`Force Removal Strategy` the drop-down menu options.

.. admonition:: Priority

   When there are different removal strategies applied on the location and product category for a
   product, the *force* removal strategy set on the :guilabel:`Product Category` is applied.

.. image:: removal/navigate-location-category.png
   :align: center
   :alt: Change the Force Removal Strategy for either the Product Categories or Locations.

Required features
-----------------

While some removal strategies are available by default, some additional features **must** be enabled
in :menuselection:`Inventory --> Configuration --> Settings` for the removal strategy option to
appear in the drop-down menu of the :guilabel:`Force Removal Strategy` or :guilabel:`Removal
Strategy` field.

Refer to the table below for a summary of required features. Otherwise, refer to the dedicated
sections for the removal strategy for more details on requirements and usage.

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * -
     - :ref:`FIFO <inventory/removal/fifo>`
     - :ref:`LIFO <inventory/removal/lifo>`
     - :ref:`FEFO <inventory/removal/fefo>`
     - :ref:`Closest Location <inventory/removal/close>`
     - :ref:`Least Packages <inventory/removal/package>`
   * - Required features
     - Lots & Serial Numbers
     - Lots & Serial Numbers
     - Lots & Serial Numbers, Expiration Date
     - Storage Locations, Multi-Step Routes
     - Packages

.. _inventory/removal/lots-setup:

Lots and serial numbers
~~~~~~~~~~~~~~~~~~~~~~~

Lots and serial numbers differentiate identical products and track information like arrival or
expiration dates. To enable this feature, navigate to :menuselection:`Inventory --> Configuration
--> Settings`. Under the :guilabel:`Traceability` heading, check the box beside :guilabel:`Lots &
Serial Numbers` to enable the feature.

.. image:: removal/enable-lots.png
   :align: center
   :alt: Enable lots and serial numbers.

Next, ensure the intended product is tracked by lots or serial numbers by navigating to the product
form through :menuselection:`Inventory --> Products --> Products` and selecting the desired product.
On the product form, switch to the :guilabel:`Inventory` tab, and under the :guilabel:`Tracking`
field, select either the :guilabel:`By Unique Serial Number` or :guilabel:`By Lots` options.

Expiration date
~~~~~~~~~~~~~~~

Enable the **expiration date** to track expiration dates, best before dates, removal dates, and
alert dates on a lot or serial number. This feature is only available with lots and serial numbers
enabled.

.. image:: removal/enable-expiration.png
   :align: center
   :alt: Enable expiration dates feature for FEFO.

Locations and routes
~~~~~~~~~~~~~~~~~~~~

**Storage locations** and **multi-step routes** are necessary features for setting **all** types of
removal strategies on a location. However, these features are specifically required for the closest
location removal strategy since it is only applied at the location level.

To activate these features, navigate to :menuselection:`Inventory --> Configuration --> Settings`.
Under the :guilabel:`Warehouse` heading, enable the :guilabel:`Storage Location` and
:guilabel:`Multi-Step Routes` features.

.. image:: removal/enable-location.png
   :align: center
   :alt: Enable the locations and route features.

Packages
~~~~~~~~

The *packages* feature is used to group products together and is required for the least packages
removal strategy.

.. image:: removal/enable-pack.png
   :align: center
   :alt: Enable the packages feature.

.. seealso::
   - :ref:`Packages <inventory/management/packages>`
   - :doc:`2-step delivery <../../shipping_receiving/daily_operations/receipts_delivery_two_steps>`
   - :doc:`3-step delivery <../../shipping_receiving/daily_operations/delivery_three_steps>`

.. _inventory/removal/fifo:

First in, first out (FIFO)
==========================

The *first in, first out* (FIFO) removal strategy selects products with the earliest arrival dates.
This method is useful for companies selling products with short demand cycles, like clothes, to
prevent prolonged stock retention of specific styles.

.. example::
   Various quantities of the product, `T-shirt`, tracked by lot numbers, arrive on August 1st and
   August 25th. For an order made on September 1st, the :abbr:`FIFO (First In, First Out)` removal
   strategy  prioritizes lots that have been in stock the longest. So, products received on August
   1st are selected first for picking.

   .. image:: removal/fifo-example.png
      :align: center
      :alt: Illustration of FIFO selecting the oldest products in stock.

To use the :abbr:`FIFO (First In, First Out)` removal strategy, enable the :guilabel:`Lots & Serial
Numbers` feature and activate :guilabel:`Tracking` by lots or serial numbers on the product form.

.. seealso::
   :ref:`Lot/serial number setup details <inventory/removal/lots-setup>`

.. _inventory/removal/arrival_date:

Arrival date
------------

Check the lot or serial number's earliest arrival date of each product by going to
:menuselection:`Inventory --> Products --> Lots/Serial Numbers`. Then, select the :guilabel:`▶️
(right-pointing arrow)` on the left of a product line to reveal a list of lots or serial numbers of
the product in stock. The :guilabel:`Created On` field shows the lot/serial number creation date,
which is essentially the arrival date.

.. example::
   Serial number `00000000500` of the product, `Cabinet with Doors` arrived on December 29th, as
   displayed in the :guilabel:`Created On` field.

   .. image:: removal/created-on.png
      :align: center
      :alt: Display arrival date of a lot for an item.

Workflow
--------

To understand how :abbr:`FIFO (First In, First Out)` rotates products out, consider there are three
lots of white shirts. The shirts are from the *All/Clothes* category, where :abbr:`FIFO (First In,
First Out)` is set as the :guilabel:`Force Removal Strategy`.

The white shirts are tracked :guilabel:`By Lots` in the :guilabel:`Inventory` tab of the product
form.

.. seealso::
   - :ref:`Set up force removal strategy <inventory/routes/strategies/set>`
   - :ref:`Enable lots tracking <inventory/removal/lots-setup>`

The following table represents the white shirt's on-hand stock and lot number details relating to
this example.

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * -
     - LOT1
     - LOT2
     - LOT3
   * - On-hand stock
     - 5
     - 3
     - 2
   * - :ref:`Created on <inventory/removal/arrival_date>`
     - March 1
     - April 1
     - May 1

To see the removal strategy in action, create a :ref:`delivery order <inventory/delivery/one-step>`
for six white shirts, by either going to the :menuselection:`Sales app` and create a new quotation,
or from the delivery orders dashboard in :menuselection:`Inventory --> Operations --> Deliveries`.
:guilabel:`Confirm` the sales order or click :guilabel:`Mark as Todo` on the draft delivery order.

Doing so creates the delivery order, and the oldest lot numbers are reserved thanks to the
:abbr:`FIFO (First In, First Out)` removal strategy.

To view the detailed pickings, click the :guilabel:`⦙≣ (bulleted list)` icon on the far right of the
white shirt's product line in the :guilabel:`Operations` tab of the delivery order. Doing so opens
the :guilabel:`Stock move` pop-up window.

In the :guilabel:`Stock move` window, the :guilabel:`Pick from` field details where the quantities
to fulfill the :guilabel:`Demand` are picked from. Since the order demanded six shirts, all five
shirts from `LOT1` and one shirt from `LOT2` are selected.

.. image:: removal/white-shirt-picking.png
   :align: center
   :alt: Two lots being reserved for a sales order with the FIFO strategy.

.. _inventory/removal/lifo:

Last in, first out (LIFO)
=========================

Similar to the :ref:`FIFO removal strategy <inventory/removal/fifo>`, the *last in, first out*
(LIFO) removal strategy picks products based on the date they entered a warehouse's stock. Instead
of removing the oldest stock on-hand, however, it targets the **newest** stock on-hand for removal.

Every time an order for products with the :abbr:`LIFO (Last In, First Out)` method is placed, a
transfer is created for the lot/serial number that has most recently entered the stock (the **last**
lot/serial number that entered the warehouse's inventory).

.. warning::
   In many countries, the :abbr:`LIFO (Last In, First Out)` removal strategy in banned, since it can
   potentially result in old, expired, or obsolete products being delivered to customers.

Consider the following product, `Cinder Block`, which is tracked :guilabel:`By Lots` in the
:guilabel:`Inventory` tab of the product form, and its product category's :guilabel:`Force Removal
Strategy` is set to :guilabel:`Last In, First Out (LIFO)`.

.. seealso::
   - :ref:`Set up force removal strategy <inventory/routes/strategies/set>`
   - :ref:`Enable lots tracking <inventory/removal/lots-setup>`
   - :ref:`Check arrival date <inventory/removal/arrival_date>`

The following table represents the cinder blocks in stock and their various lot number details.

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * -
     - LOT1
     - LOT2
     - LOT3
   * - On-hand stock
     - 10
     - 10
     - 10
   * - :ref:`Created on <inventory/removal/arrival_date>`
     - June 1
     - June 3
     - June 6

To see the removal strategy in action, create a :ref:`delivery order <inventory/delivery/one-step>`
for seven cinder blocks, by either going to the :menuselection:`Sales app` and create a new
quotation, or from the delivery orders dashboard in :menuselection:`Inventory --> Operations -->
Deliveries`. :guilabel:`Confirm` the sales order or click :guilabel:`Mark as Todo` on the draft
delivery order.

Doing so creates the delivery order, and the newest lot numbers are reserved thanks to the
:abbr:`LIFO (Last In, First Out)` removal strategy.

To view the detailed pickings, click the :guilabel:`⦙≣ (bulleted list)` icon on the far right of the
cinder block's product line in the :guilabel:`Operations` tab of the delivery order. Doing so opens
the :guilabel:`Stock move` pop-up window.

In the :guilabel:`Stock move` window, the :guilabel:`Pick from` field details where the quantities
to fulfill the :guilabel:`Demand` are picked from. Since the order demanded seven cinder blocks, the
newest cinder blocks from `LOT3` are selected using the :abbr:`LIFO (Last In, First Out)` removal
strategy.

.. image:: removal/cinder-block-picking.png
   :align: center
   :alt: The detailed operations shows which lots are being selected for the picking.

.. _inventory/removal/fefo:

First expired, first out (FEFO)
===============================

The *first expired, first out* (FEFO) removal strategy targets products for removal based on their
assigned removal dates.

.. _inventory/removal/removal-date:

Removal date
------------

A *removal date* is a certain number of days before the product's *expiration date* on which the
product needs to be removed from stock. This number of days is set by the user by navigating to the
product form's :guilabel:`Inventory` tab. Under the :guilabel:`Traceability` section, ensure the
:guilabel:`Tracking` is set to either :guilabel:`By Lots` or :guilabel:`By Unique Serial Number`.

Next, check the :guilabel:`Expiration Date` option, which makes the :guilabel:`Removal Date` and
other dates appear.

.. important::
   The :guilabel:`Lots and Serial Numbers` and :guilabel:`Expiration Dates` features **must** be
   enabled in :menuselection:`Inventory app --> Configuration --> Settings` to track expiration
   dates.

The expiration date of a product is determined by adding date the product was received to the number
of days specified in the :guilabel:`Expiration Date` of the product form. The removal date takes
this expiration date and subtracts the number of days specified in the :guilabel:`Removal Date` of
the product form.

.. note::
   For more information about expiration dates, reference the :doc:`Expiration dates
   <../../product_management/product_tracking/expiration_dates>` document.

.. example::
   In the :guilabel:`Inventory` tab of the product, egg, the following :guilabel:`Dates` are set by
   the user:

   - :guilabel:`Expiration Date`: `30` days after receipt
   - :guilabel:`Removal Date`: `15` days after expiration date

   .. image:: removal/user-set-date.png
      :align: center
      :alt: Display expiration and removal dates set on the product form.

   Eggs, received from the vendor, arrive at the warehouse on January 1st. So, the expiration date
   of the eggs is **January 31st** (Jan 1st + 30). By extension, the removal date is **January
   16th** (Jan 31 - 15).

.. _inventory/removal/exp-date:

To view the expiration dates of items in stock, navigate to the product form and click the
:guilabel:`On Hand` smart button.

Next, click the additional options icon on the far right and select the columns
:guilabel:`Expiration Date` and :guilabel:`Removal Date`.

.. image:: removal/removal-date.png
   :align: center
   :alt: Show expiration dates from the inventory adjustments model accessed from the *On Hand*
         smart button from the product form.

Workflow
--------

Using the :abbr:`FEFO (First Expired, First Out)` removal strategy, every sales order that includes
products with this removal strategy assigned ensures that transfers are requested for products with
the expiration date soonest to the order date.

To understand how this removal strategy works, consider the following example below about the
product, `Egg carton`, which is a box containing twelve eggs. The product is tracked :guilabel:`By
Lots`, and the product category's :guilabel:`Force Removal Strategy` is set to :guilabel:`First
Expired, First Out (FEFO)`

.. seealso::
   - :ref:`Set up force removal strategy <inventory/routes/strategies/set>`
   - :ref:`Enable lots tracking <inventory/removal/lots-setup>`
   - `Odoo Tutorials: Perishable Products <https://www.youtube.com/watch?v=8zAlNcdg0ig>`_

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * -
     - LOT1
     - LOT2
     - LOT3
   * - On-hand stock
     - 5
     - 2
     - 1
   * - Expiration date
     - April 4
     - June 20
     - July 1
   * - :ref:`Removal date <inventory/removal/exp-date>`
     - February 26
     - May 11
     - May 22

To see the removal strategy in action, create a :ref:`delivery order <inventory/delivery/one-step>`
for six cartons of eggs, by either going to the :menuselection:`Sales app` and create a new
quotation, or from the delivery orders dashboard in :menuselection:`Inventory --> Operations -->
Deliveries`. :guilabel:`Confirm` the sales order or click :guilabel:`Mark as Todo` on the draft
delivery order.

Doing so creates the delivery order for today, December 29th, and the lot numbers with the soonest
expiration dates are reserved thanks to the :abbr:`FEFO (First Expired, First Out)` removal
strategy.

To view the detailed pickings, click the :guilabel:`⦙≣ (bulleted list)` icon on the far right of the
egg's product line in the :guilabel:`Operations` tab of the delivery order. Doing so opens
the :guilabel:`Stock move` pop-up window.

In the :guilabel:`Stock move` window, the :guilabel:`Pick from` field details where the quantities
to fulfill the :guilabel:`Demand` are picked from. Since the order demanded six cartons of eggs,
using the :abbr:`FEFO (First Expired, First Out)` removal strategy, all five cartons from `LOT1`
with the removal date of February 26th are picked. The remaining carton is selected from the `LOT2`,
which has a removal date of May 11.

.. image:: removal/eggs-picking.png
   :align: center
   :alt: The stock moves window that shows the lots to be removed using FEFO.

.. _inventory/removal/close:

Closest location
================

For the *closest location* removal strategy, products are picked based on alphanumeric order of the
storage location's name. This strategy requires businesses to store products that are ordered most
often in locations closest to the output area. Then, these locations are named in alphanumeric order
with the closest locations starting with letters closest to the beginning of the alphabet.

The aim is to save the warehouse worker from taking a long journey to a farther shelf when the
product is also available at a closer location.

.. _inventory/removal/sequence:

To understand *location sequence* in the closest removal strategy, consider the following example
below.

.. example::
   A product is stored in the following locations: `Shelf A/Pallet`, `Shelf A/Rack 1` and `Shelf
   A/Rack 2`.

   .. image:: removal/locations.png
      :align: center
      :alt: Show a mockup of real storage location in a warehouse.

   The sublocation `Pallet` is on the ground level, so products stored here are easier to retrieve,
   compared to requiring a forklift to reach `Rack 1` and `Rack 2`. The storage locations were
   strategically named in alphabetic order based on ease of access.

.. important::
   To use this removal strategy, the :guilabel:`Storage Locations` and :guilabel:`Multi-Step Routes`
   settings **must** be enabled in :menuselection:`Inventory --> Configuration --> Settings`.

Location names
--------------

Create new or rename locations by navigating to :menuselection:`Inventory --> Configuration -->
Locations`. Select the desired location and type the :guilabel:`Location Name`.

Once the locations are named in alphabetical order based on the location's proximity from the output
or packing location, set the removal strategy on the parent location. To do that, in the
:guilabel:`Locations` list, select the parent location of the alphabetically named storage
locations.

Doing so opens the form for the parent location. In the :guilabel:`Removal Strategy` field, select
:guilabel:`Closest Location`.

.. example::
   In a warehouse, the storage location `WH/Stock/Shelf 1` is located closest to the packing area,
   where products retrieved from shelves are packed for shipment. The popular product, `iPhone
   charger` is stored in three locations, `WH/Stock/Shelf 1`, `WH/Stock/Shelf 2`, and
   `WH/Stock/Shelf 3`.

   To use closest location , set the removal strategy on the parent location, 'WH/Stock'.

Workflow
--------

To see how the closest location removal strategy works, consider the popular product, `iPhone
charger` that is stored in `WH/Stock/Shelf 1`, `WH/Stock/Shelf 2`, and `WH/Stock/Shelf 3`. There are
fifteen, five, and thirty units in stock at each respective location.

.. tip::
   To check the on-hand stock at each storage location, navigate to the product form and click the
   :guilabel:`On Hand` smart button.

   .. image:: removal/on-hand-stock.png
      :align: center
      :alt: Show on-hand stock at all locations.

Create a :ref:`delivery order <inventory/delivery/one-step>` for eighteen units of the `iPhone
charger`, by either going to the :menuselection:`Sales app` and create a new quotation, or from the
the delivery orders dashboard in :menuselection:`Inventory --> Operations --> Deliveries`.

On the delivery order, the :guilabel:`Quantity` field displays the amount automatically picked
according to the removal strategy. For more details about *where* the units were picked, select the
:guilabel:`⦙≣ (bulleted list)` icon on the far right. Doing so opens the :guilabel:`Stock move`
pop-up window that displays how the reserved items were picked according to the removal strategy.

In the :guilabel:`Stock move` window, the :guilabel:`Pick from` field details where the quantities
to fulfill the :guilabel:`Demand` are picked from. All fifteen of the units stored at the closest
location, `WH/Stock/Shelf 1` are picked first. The remaining three units are then selected from the
second closest location, `WH/Stock/Shelf 2`.

.. image:: removal/stock-move-window.png
   :align: center
   :alt: Display *Pick From* quantities for the order for iPhone chargers.

.. _inventory/removal/package:

Least packages
==============

The *least packages* removal strategy fulfills an order by opening the fewest number of packages,
ideal for maintaining organized stock without multiple open boxes.

To understand how the removal strategy works, consider how a warehouse stores packages of flour
in bulk. The product is purchased from the vendor in packages measured `10 kg`, `30 kg`, `50 kg`.

Then, the flour is stored in a sealed package in quantities of `100 kg`. To minimize moisture or
pests from entering open packages, the least packages removal strategy is used to pick from a
single, opened package.

.. example::
   A package of `100 kg` of flour is depleted to `54 kg` after fulfilling some orders. There are
   other packages of `100 kg` in stock.

   #. When an order for `14 kg` of flour is placed, the package of 54 kg is selected.
   #. However, when the order exceeds an amount the `54 kg` package, one of the packages of `100 kg`
      is used to fulfill the order.

Workflow
--------

To use the removal strategy, enable the *Packages* feature by navigating to
:menuselection:`Inventory --> Configuration --> Settings`. Then, check the box beside
:guilabel:`Packages` to enable the feature.

Then, set the removal strategy on the :ref:`product category or storage location
<inventory/routes/strategies/set>`.

To see how the least packages removal strategy works, consider the product, `Flour`, in the
following example. The product's :guilabel:`Units of Measure` field on the product form set to `kg`.
The product is stored in packages of one hundred kilograms, with one package with `54 kg` remaining.

.. tip::
   To check the product's on-hand stock, navigate to the product form and click the :guilabel:`On
   Hand` smart button.

   .. image:: removal/on-hand-flour.png
      :align: center
      :alt: Show on-hand stock in each package.

Navigate to the product category, `Wheats`, by going to :menuselection:`Inventory --> Configuration
--> Product Categories` and selecting the desired category. On the product category form, set the
:guilabel:`Force Removal Strategy` to :guilabel:`Least Packages`.

.. image:: removal/set-least-packages.png
   :align: center
   :alt: Set least packages removal strategy on the product category.

Create a :ref:`delivery order <inventory/delivery/one-step>` for eighty kilograms of flour, by
either going to the :menuselection:`Sales app` and create a new quotation, or from the delivery
orders dashboard in :menuselection:`Inventory --> Operations --> Deliveries`.

On the delivery order, the :guilabel:`Quantity` field displays the amount automatically picked
according to the removal strategy. For more details about *where* the units were picked, select the
:guilabel:`⦙≣ (bulleted list)` icon on the far right. Doing so opens the :guilabel:`Stock move`
pop-up window that displays how the reserved items were picked according to the removal strategy.

In the :guilabel:`Stock move` window, the :guilabel:`Pick from` field details where the quantities
to fulfill the :guilabel:`Demand` are picked from. Since the order demanded eighty kilograms, which
exceeds the quantity in the opened package of `54 kg`, an unopened package of `100 kg` is selected.

.. image:: removal/least-package.png
   :align: center
   :alt: Show which package was picked in the *Pick From* field.

Doing so allows the warehouse employees to consolidate the remaining `20 kg` of flour from the `100
kg` package with the `54 kg`, instead of picking the `54 kg` package, and picking the remaining `26
kg` from another sealed package.
