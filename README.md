# shmera

<button type="button" class="btn btn-success" data-bs-toggle="modal"
        data-bs-target="#EditEmailModal"
        data-email-id="@email.Id"
        data-email-address="@email.EmailAddress"
        data-email-type-id="@email.EmailTypeId"
        data-customer-id="@Model.Id">
    Edit
</button>


<script>
    document.addEventListener('DOMContentLoaded', function () {
        // Βρίσκουμε όλα τα κουμπιά "Edit" που ανοίγουν το modal
        const editButtons = document.querySelectorAll('button[data-bs-target="#EditEmailModal"]');

        editButtons.forEach(button => {
            button.addEventListener('click', function () {
                // Παίρνουμε τις τιμές από τα data-attributes του κουμπιού
                const emailId = button.getAttribute('data-email-id');
                const emailAddress = button.getAttribute('data-email-address');
                const emailTypeId = button.getAttribute('data-email-type-id');
                const customerId = button.getAttribute('data-customer-id');

                // Τοποθετούμε τις τιμές στα input πεδία του modal
                document.getElementById('email-id').value = emailId;
                document.getElementById('email-address').value = emailAddress;
                document.getElementById('email-type-id').value = emailTypeId;
                document.getElementById('customer-id').value = customerId;
            });
        });
    });
</script>

@model PhoneBook.Models.Email

<!-- Το μοναδικό modal -->
<div class="modal fade" id="EditEmailModal" tabindex="-1" aria-labelledby="EditEmailLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="EditEmailLabel">Edit Email</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <form asp-controller="Customers" asp-action="EditEmail" method="post">
                    <div asp-validation-summary="ModelOnly" class="text-danger"></div>

                    <input type="hidden" id="email-id" name="Id" />
                    <input type="hidden" id="customer-id" name="CustomerId" />

                    <div class="mt-3">
                        <label for="email-address" class="control-label">Email Address</label>
                        <input id="email-address" name="EmailAddress" class="form-control" />
                    </div>

                    <div class="mt-3">
                        <label for="email-type-id" class="control-label">Email Type</label>
                        <select id="email-type-id" name="EmailTypeId" class="form-control" asp-items="ViewBag.EmailTypeId"></select>
                    </div>

                    <div class="mt-3">
                        <input type="submit" value="Edit" class="btn btn-primary" />
                    </div>
                </form>
            </div>
        </div>
    </div>
</div>

