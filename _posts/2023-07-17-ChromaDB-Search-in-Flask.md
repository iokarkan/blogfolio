---
layout: post
title: "Full-text search in Flask with ChromaDB and embeddings"
tags: flask web development embeddings
icon: "fas fa-hammer"
---

<div class="mt-6 border-2 rounded-xl flex max-w-xl flex-row m-auto justify-center">
  <?xml version="1.0" encoding="utf-8"?>
  <!-- Uploaded to: SVG Repo, www.svgrepo.com, Generator: SVG Repo Mixer Tools -->
  <svg fill="#000000" width="160px" height="160px" viewBox="0 0 32 32" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <title>(Flask</title>
    <path
      d="M14.319 9.028c0.35-0.62-1.443-0.835-0.235-0.219 0.112 0.037 0.087 0.262 0.235 0.219zM4.542 3.761c-0.762-0.995 1.432 0.167 0.659-0.875-0.652-0.519-1.278 0.585-0.659 0.875zM6.138 5.011c1.082-0.144-0.275-0.466-0.217-0.013zM5.283 4.806c0.232-0.315-0.407 0.16 0 0zM7.008 6.705c0.672 0.016-0.289-0.902 0.511-0.487-0.131-0.429-0.932-0.509-1.325-0.68-0.22 0.392 0.45 1.172 0.812 1.167zM4.916 6.619c0.575-0.434 1.984 0.257 1.080-0.431-0.087-0.077-1.982 0.522-1.080 0.431zM4.326 7.747c1.007-0.342 2.383-0.726 2.858 0.169-0.484-0.582-0.195-1.155 0.262-0.304 0.645 0.861 0.968-0.391 0.547-0.681 0.479 0.595 1.023 0.875 0.321 0.037 0.762-0.917-1.528 0.121-2.049 0.11-0.25 0.112-2.588 0.596-1.938 0.669zM6.2 10.881c0.246-0.304-0.337-0.081 0 0zM5.613 12.452c-0.060-0.362-0.175 0.192 0 0zM5.116 12.2c0.562-0.037 0.882-0.621-0.109-0.587-1.537-0.159 1.355 0.525-0.197 0.33-0.209 0.137 0.295 0.296 0.306 0.259zM29.116 27.445c0.696 0 2.109-0.216 0.594-0.216-0.237 0.038-1.386 0.030-0.595 0.216zM25.78 25.486c0.075-0.51-0.337 0.046 0 0zM28.395 27.273c0.015-0.444-0.38 0.2 0 0zM2.65 11.165c0.499-0.381-0.589-0.145 0 0zM4.549 12.515c0.306-0.325-0.663-0.132 0 0zM3.906 12.335c0.871-0.534-0.926-0.462 0 0zM10.348 8.28c0.291-0.765 1.132-0.306 0.135-0.154 0.021 0.081-0.030 0.395-0.135 0.154zM9.548 8.285c-0.069-1.517 1.398 0.54-0 0zM6.736 8.718c0.462-0.555 2.618-0.354 1.040-0.054-0.422-0.319-0.747 0.187-1.040 0.054zM6.541 8.848c0.277-0.325 0.080 0.287-0 0zM5.782 9.154c0.040-0.514 1.272 0.272 0.204 0.185zM5.226 9.144c0.437-0.325 0.232 0.182-0 0zM5.167 9.687c0.304-1.117 1.625 0.918 0.497 0.147-0.121-0.095-0.275-0.152-0.443-0.152-0.019 0-0.038 0.001-0.057 0.002l0.002-0zM2.050 11.274c-0.116-0.669-0.1-1.842 1.015-1.445-1.488 0.295 1.030 1.849 0.712 0.622 0.625 0.030 1.225-0.37 0.895 0.237 1.233-0.137 2.087-1.205 3.279-1.056 1.082-0.090 2.082-0.299 3.033-0.615l-0.091 0.026c0.822-0.060 1.612-0.945 1.162-1.468-0.218-0.013-0.473-0.021-0.73-0.021-0.993 0-1.96 0.114-2.888 0.329l0.086-0.017c-1.372 0.285-2.619 0.827-4.005 1.061-1.35 0.181 0.271 0.5-0.115 0.57-0.705 0.245 0.84 0.41-0.091 0.667-0.575-0.11-1.175-0.307-0.928-0.912-1.293 0.166-2.431 0.704-1.408 2.019h0.075zM4.22 12.726c0.069-0.475-0.512 0.094-0 0zM26.941 27.412c0.165-0.49-0.417 0.062 0 0zM24.474 26.133c0.412-0.379-0.525-0.117 0 0zM4.062 13.526c0.647-0.254-1.175-0.525-0.13-0.050zM2.538 12.615c-0.044-0.4-0.237 0.050 0 0zM2.263 12.823c-0.025-0.337-0.18 0.127 0 0zM4.12 14.028c-0.087-0.731-1.050-0.11 0-0zM7.719 16.687c0.152-0.14-0.362-0.104 0 0zM4.463 14.6c-0.15-0.121-0.117 0.152 0 0zM3.946 14.347c0.011-0.312-0.829-0.28 0 0zM3.041 14.119c-0.172-0.968-0.656-0.147-0 0zM6.836 16.754c0.011-0.509-0.396-0.019 0 0zM23.985 27.436c0.64-0.13 2.097 0.325 2.332-0.17-0.775-0.019-2.687-0.547-2.777 0.125l0.17 0.029zM6.378 16.639c-0.009-0.166-0.152 0.062 0 0zM4.933 15.939c0.499-0.169-0.459-0.112 0 0zM16.467 23.725c-0.009-0.501-0.494 0.125 0 0zM5.241 16.65c0.775-0.3-0.83-0.212 0 0zM20.249 26.297c0.27-0.2-0.337-0.025 0 0zM17.435 24.523c-0.050-0.194-0.196 0.037 0 0zM17.093 24.274c-0.135-0.347-0.535-0.008 0 0zM9.994 19.796c0-0.506-0.906-0.205 0 0zM9.174 19.606c-0.332-0.279-0.016-0.040 0 0zM3.771 16.275c0.115-0.479-1.066-2.633-0.557-1.080 0.182 0.325 0.162 0.942 0.557 1.080zM6.715 18.599c0.646 0.145 2.582 1.592 1.44 0.1-0.585-0.172-0.234-1.603-0.831-1.35 0.4 0.669 0.33 0.953-0.512 0.532-1.056-0.516-0.592 0.255-0.387 0.467-0.28 0.065 0.374 0.245 0.291 0.25zM22.891 29.012c0.482-0.322-0.586-0.104 0 0zM21.166 27.865c0.717-0.602-0.759 0.266-0 0zM21.503 28.028c0.881-0.637-0.535-0.122-0.185 0.12zM11.639 22.174c-0.181-0.371-0.28 0.059 0 0zM11.064 21.841c-0.025-0.3-0.364 0.025 0 0zM20.399 27.727c0.689-0.444-0.157-0.375-0.125 0.040zM6.272 18.818c0.204-0.302-0.525-0.039 0 0zM20.625 28.018c0.712-0.61-0.45-0.128 0-0zM19.543 27.593c1.418-0.917-0.582-0.4 0-0zM4.51 18.178c-0.657-0.937-0.409-1.36-1.043-2.124-0.12-0.587-1.087-1.916-0.5-0.507 0.537 0.823 0.697 2.098 1.543 2.632zM19.784 27.853c0.771-0.817-0.747 0.049 0 0zM19.783 28.115c0.004-0.187-0.3 0.082-0 0zM18.333 27.121c0.697-0.585-0.675 0.26-0 0zM11.964 23.185c0.452 0.4 2.077 0.295 0.55 0.050-0.227-0.337-1.438-0.255-0.55-0.050zM7.327 20.39c-0.302-0.502-1.080-0.455 0 0zM6.513 19.855c-0.125-0.491-0.875-0.487 0-0zM18.624 27.462c0.406-0.394 0.016 0.629 0.675-0.096 0.006-0.519-0.021-0.825-0.757-0.195-0.202 0.112-0.292 0.591 0.082 0.291zM17.861 27.141c0.025-0.35-0.241 0.3 0-0zM10.438 22.644c1.762 0.567-0.864-0.695 0-0zM8.988 21.811c0.425 0.316 1.6 0.898 0.605 0.12 0.336-0.39-0.642-0.597-0.317-0.857-0.825-0.505-0.65-0.46-0.072-0.445-0.992-0.442 0.142-0.41 0.087-0.637-0.381-0.075-1.899-0.675-1.005 0.050-0.907-0.462-0.216 0.172-0.49 0.105-0.928-0.252 0.825 0.706-0.147 0.469 0.531 0.421 1.432 1.080 0.225 0.446-0.16 0.229 0.862 0.575 1.115 0.75zM11.726 23.628c0.769 0.2 0.765-0.119 0.069-0.212-0.375-0.35-1.557-0.719-0.5-0.044 0.071 0.177 0.294 0.174 0.43 0.257zM10.339 22.928c-0.16-0.139 0.020 0.087-0-0zM11.013 9.666c0.117-0.144 0.025 0.174-0-0zM10.61 12.069c-0.27-0.475 0.34-2.091 0.407-1.087-0.284 0.781-0.081 1.218 0.116 0.17 0.366-0.825-0.079 1.628-0.525 0.918zM10.218 12.706c-0.066-0.4 0.225 0.505 0 0zM10.459 13.343c-0.393-0.97 0.365 0.512-0-0zM10.623 13.706c-0.003-0.209 0.054 0.302-0-0zM7.795 12.132c0.257-0.542 0.475 0.604-0-0zM6.793 11.535c0.161-0.069 0.085 0.215-0-0zM11.076 14.879c0.146-1.18 0.129 0.691-0-0zM7.234 12.625c0.211-0.31-0.562-1.4 0.111-0.391 0.29 0.231 0.84 0.387 0.354 0.484 0.762 0.674-0.187 0.182-0.465-0.092zM11.296 15.203c0.055-1.037 0.31-0.619 0.002 0.147zM6.848 12.985c0.519-0.11 2.147 0.911 0.65 0.292-0.165-0.185-0.52-0.1-0.65-0.293zM11.586 16.261c0.162-0.577 0.012 0.381 0 0zM9.484 14.913c-0.082-1.012 0.184 0.167 0 0zM6.715 13.444c-0.871-1.203 2.533 1.216 0.559 0.305-0.206-0.054-0.455-0.075-0.559-0.305zM11.521 16.702c0.067-0.275 0.009 0.322 0 0zM11.771 16.95c0.060-0.641 0.124 0.437-0 0zM10.334 16.1c-0.587-0.352-0.154-2.479 0.046-1.025 0.571-0.185-0.031 0.75 0.394 0.742-0.066 0.591-0.257 0.804-0.437 0.282zM6.448 13.841c-1.357-1.207 1.706 0.632 0.221 0.225zM7.319 14.674c-0.41-0.771 0.5 0.322 0 0zM6.881 14.533c0.271-0.269 0.144 0.265 0 0zM6.169 14.552c-0.467-0.462-0.805-0.891 0.021-0.287 0.319 0.012-0.707-0.972 0.075-0.312 0.825 0.15 0.409 1.352-0.096 0.6zM7.524 15.601c0.27-0.569 0.457 0.792 0 0zM6.961 15.408c0.050-0.754 0.287 0.516 0 0zM8.215 16.271c-0.262-0.448-0.417-0.987-0.417-1.562 0-0.001 0-0.002 0-0.003v0c0.095 0.472 1.005 2.033 0.446 0.647-0.617-1.162 0.737 0.377 0.877 0.667 0.062 0.287-0.381-0.079-0.080 0.597-0.55-0.771-0.325 0.425-0.826-0.347zM12.271 18.977c-0.44-0.987 0.312-0.54 0.097 0.162zM9.919 18.222c-0.194-0.347 0.404 0.325 0 0zM12.658 20.128c0.168-0.63 0.198 0.53 0 0zM8.78 18.026c0.274-0.075 0.135 0.467 0 0zM13.653 21.39c-0.465-0.9 0.587 0.255 0 0zM14.056 21.931c-0.012-0.585 0.134 0.45 0 0zM18.687 25.45c0.231-0.014 0.008 0.175 0 0zM14.64 22.879c-0.37-0.387-0.466-1.112-0.066-0.481 0.205 0.082 0.656 1.183 0.066 0.481zM15.883 26.388c0.966-0.577 0.647 1.352 1.638 0.162 0.977-0.712-0.843 0.883 0.362 0.129 0.87-0.584 2.157 0.275 2.969 0.556 0.585-0.029 1.153 0.506 1.753 0.181 1.153-0.312-2.257-0.462-1.362-1.012-0.138 0.031-0.297 0.049-0.46 0.049-0.805 0-1.509-0.435-1.89-1.082l-0.006-0.010c-1.299-0.215-2.402-0.92-3.136-1.914l-0.009-0.013c-0.24-0.394 0.35 0.055-0.207-0.587-0.606-0.61-1.123-1.311-1.527-2.079l-0.023-0.047c-0.571-0.305-0.637-1.203-0.696-0.030 0.005-0.741-0.691-1.24-0.86-1.032-0.002-0.714 0.744-0.356 0.22-0.884-0.112-0.74-0.482-1.512-0.594-2.346-0.172-0.402-0.025-1.263-0.591-0.352-0.206 0.962-0.069-1.183 0.252-0.475 0.421-0.725-0.15-0.637-0.175-0.537 0.275-0.61 0.175-1.475-0.071-1.145 0.146-0.646 0.231-2.377-0.219-2.069 0.272-0.675 0.517-3.090-0.667-2.169-0.62 0.025-1.202 0.159-1.736 0.382l0.033-0.012c1.232 0.679-0.125 0.245-0.625 0.137-0.065 0.627-0.562 0.356-1.182 0.362 0.991 0.122-0.482 1.012-1.051 0.667-0.737 0.352 0.637 1.233 0.015 1.506 0.075 0.41-1.131-0.15-1.037 0.8-0.716-0.301-0.097 1.125 0.261 0.642 1.218 0.33 0.857 1.082 0.887 1.796-0.197 0.416-0.98-0.978-0.175-0.914-0.634-1.033-0.701-0.375-1.23 0.106-0.125 0.035 1.348 0.684 0.425 1.003 0.812 0.125 0.835 0.837 1 1.287 0.487 0.509 0.387-0.562 0.973 0.050-0.37-0.545-1.958-1.535-0.68-1.217-0.006-0.55-0.231-0.991 0.161-0.98 0.387-0.702-0.406 1.733 0.469 0.84 0.241-0.106 0.3-0.704 0.737 0.056 0.631 0.622 0.227 1.072-0.664 0.504 0.159 0.541 1.192 0.734 0.998 1.581 0.206 0.744 0.494 0.47 0.745 0.427 0.197 0.722 0.309 0.191 0.319-0.154 0.9 0.194 0.69 0.725 0.972 1.1 0.621 0.28-0.89-1.902 0.177-0.657 1.122 1.012 0.421 1.437-0.587 1.275 0.637-0.051 0.844 0.862 1.641 0.83 0.727 0.346 1.218 1.675-0.034 1.121-0.435-0.391-1.974-0.875-0.716-0.13 1.282 0.525 2.335 1.039 3.35 1.611l-0.15-0.077c0.8 0.572 1.147 1.227 1.45 1.357-0.672 0.321-2.028-0.257-1.021-0.435-0.629-0.114-1.335-0.431-0.734 0.35 0.512 0.429 1.812 0.382 2.046 0.431-0.199 0.435-0.537 0.47 0.008 0.504-0.607 0.325 0.195 0.375 0.251 0.56zM12.289 24.179c1.033 0.132-1.231-0.704-0.226-0.075zM15.045 26.050c0.897-0.356-0.875-0.175 0 0zM9.746 22.754c0.575-0.062-0.925-0.389 0 0zM12.877 24.744c0.075-0.319-0.66-0.096 0 0zM17.456 27.709c-0.012-0.246-0.229 0.094 0 0zM13.25 25.129c-0.142-0.162-0.068 0.035 0 0zM6.493 20.836c-0.096-0.371-0.842-0.667 0 0zM9.067 22.501c0.775-0.046-1.060-0.341 0 0zM11.239 24.068c-0.080-0.239-0.42-0.010 0 0zM17.025 27.637c0.035-0.454-0.441 0.337 0 0zM8.94 22.657c-0.052-0.25-0.332 0.023 0 0zM14.743 26.356c1.35 0.012-1.218-0.184 0 0zM12.277 24.931c1.425 0.404-1.197-0.9-0.351-0.147l0.187 0.085 0.162 0.062zM13.507 25.91c0.241-0.412-1.018-0.237 0 0zM9.458 23.438c0.582 0.447 2.349 0.057 0.892-0.266-0.662-0.354-2.158-0.595-1.14 0.212zM12.687 25.653c0.537-0.202-0.87-0.204 0 0zM11.48 24.912c0.375-0.262-0.776-0.2 0 0zM10.043 24.075c-0.050-0.209-0.77-0.231 0 0zM14.943 27.892c0.496 0.312 2.899 0.687 1.393 0.129-0.25 0.052-2.787-0.717-1.395-0.129zM11.856 25.965c-0.017-0.207-0.22 0.094 0 0zM11.239 25.657c0.609-0.394-0.787-0.005 0 0zM13.947 27.548c0.239-0.352-0.762-0.134 0 0zM12.538 26.761c0.39-0.375-0.605-0.235 0 0zM11.714 26.417c-0.067-0.331-0.3 0.185 0 0zM11.056 26.177c0.269-0.12-0.387-0.15 0 0zM6.115 21.807c0.041-0.182 0.221 0.396 0 0zM9.606 25.64c1.212 0.449-0.005-0.852-0.562-0.777-0.245-0.426-0.938-0.696-0.45-0.925-0.88 0.305-0.921-1.162-1.337-0.953-0.93-0.294-0.362-1.337-1.47-1.974-0.101-0.675-1.102-1.26-1.422-2.277-0.141-0.52-1.131-2.016-0.522-0.625 0.648 1.386 1.378 2.579 2.221 3.68l-0.034-0.047c0.545 1.179 1.346 2.158 2.336 2.898l0.020 0.014c0.362 0.348 0.71 0.879 1.221 0.987zM11.985 27.322c1.11 0.571 2.398 1.016 3.753 1.268l0.088 0.014c1.303 0.299 2.799 0.47 4.336 0.47 0.798 0 1.586-0.046 2.36-0.136l-0.094 0.009c-0.987-0.446-2.009 0.175-2.993-0.319-0.35 0.040-0.756 0.062-1.167 0.062-0.879 0-1.734-0.103-2.553-0.298l0.075 0.015c-1.631-0.594-2.987-1.206-4.292-1.902l0.179 0.087c-1.596-0.582 0.825 0.747 1.256 0.856 0.997 0.566-1.096-0.291-1.392-0.526-0.835-0.469-0.942-0.371-0.082 0.105 0.174 0.1 0.345 0.207 0.525 0.294zM9.967 26.447c-1.228-0.845-2.28-1.828-3.171-2.945l-0.023-0.029c-1.676-2.057-3.041-4.451-3.971-7.051l-0.053-0.168c-0.557-1.693-0.75-3.509-1.467-5.136-0.145-0.266-0.23-0.583-0.23-0.92 0-0.972 0.711-1.779 1.641-1.928l0.011-0.001c0.575-0.109 1.59-0.652 0.366-0.264-1.097 0.805-1.203-0.731-0.079-0.827 0.489-0.005 0.884-0.402 0.884-0.892 0-0.147-0.036-0.286-0.099-0.409l0.002 0.005c-0.825-0.537 1.999-1.128 0.579-1.929-1.478-1.598 2.071-1.904 1.196-0.092-0.209 1.393 2.479-0.256 1.856 1.353 0.634 0.774 2.374 0.175 2.331 1.261 0.925 0.062 1.241 0.84 2.108 0.9 0.9 0.406 2.527 0.725 2.832 1.737-0.891 0.707-2.954-1.456-3.053 0.497 0.023 3.075 0.48 6.034 1.312 8.832l-0.057-0.225c0.67 1.664 1.62 3.085 2.804 4.271l-0-0c1.079 1.202 2.376 2.182 3.834 2.884l0.074 0.032c1.16 0.548 2.508 0.98 3.918 1.228l0.097 0.014c0.56-0.429 1.55-2.021 2.422-1.35 0.041 0.755-1.735 1.578-0.084 1.495 0.97-0.292 1.642 0.75 2.441-0.19 0.735 0.871 3.057-0.557 2.533 1.225-0.707 0.455-1.739 0.18-2.448 0.807-1.168-0.584-2.099 0.522-3.393 0.382-1.271 0.231-2.734 0.363-4.228 0.363-0.044 0-0.089-0-0.133-0l0.007 0c-2.548-0.045-4.986-0.444-7.29-1.149l0.187 0.049c-1.394-0.471-2.603-1.091-3.7-1.86l0.046 0.031z"
    ></path>
  </svg>
  <span class="my-auto mx-8 text-6xl">+</span>
  <svg width="160px" height="160px" viewBox="0 0 256 164" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" preserveAspectRatio="xMidYMid">
    <title>Chroma logos)</title>
    <g>
      <ellipse fill="#FFDE2D" cx="170.666795" cy="81.9198362" rx="85.3332053" ry="81.9198362"></ellipse>
      <ellipse fill="#327EFF" cx="85.3332053" cy="81.9198362" rx="85.3332053" ry="81.9198362"></ellipse>
      <path d="M170.666795,81.9199642 C170.666795,127.163394 132.461431,163.83916 85.3330773,163.83916 L85.3330773,81.9199642 L170.666795,81.9199642 Z M85.3332053,81.9198362 C85.3332053,36.6767906 123.538185,8.95998209e-05 170.666795,8.95998209e-05 L170.666795,81.9198362 L85.3332053,81.9198362 Z" fill="#FF6446"></path>
    </g>
  </svg>
</div>


## Implementing search in Flask

Like many developers using Flask, my first steps followed on Miguel Grinberg's excellent tutorials on creating Flask web applications (you can find more info on these resources in his [blog](https://blog.miguelgrinberg.com/post/my-courses-and-books)).

One of the more advanced features showcased in his Udemy course is the integration of a full-text capable search functionality, implemented using elasticsearch (you may find a written version in Grinberg's blog [here](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xvi-full-text-search)). By running a local elasticsearch installation and initializing a connection from the Flask web app, the author populated elasticsearch indexes with duplicated text data from the app's relational database. Afterwards, utilizing a mixin class alongside the SQLAlchemy model classes, the searchable fields of the target database model could be specified and queried with a search function linking SQLAlchemy with elasticsearch queries.

While trying to implement such a search functionality during my [Journal Hub]({% link portfolio.md %}) project's early development, I had some trouble installing elasticsearch on MacOS 13 via homebrew, and since dockerizing seemed overkill at the time, I wondered what alternatives there were. Having previously worked on information-enhanced chatbot development with `langchain` (see [this post]({% link _posts/2023-04-18-chatbot-langchain-sources.md %})), I quickly realized that any **full-text query & retrieval implementation could also be done via the lightweight and open-source embeddings models** out there.

## Embedding models

I jump-started with ChromaDB and its default embeddings model, which fortunately is quite slim: the 80 MB `all-MiniLM-L6-v2` model from the [SentenceTransformers](https://www.sbert.net/) framework, available also in the HuggingFace Hub. It can embed 256-character sequences into a 384-dimensional space, and is advertised as suitable for many use cases and for basic embedding proximity/similarity searches.

Text embeddings turn words into numbers in a high-dimensional space (in this case, 384 dimensions). The dimensions can be chosen either by hand, or by creating a dictionary of unique word tokens in a dataset, or rather by training a fixed-size Embedding layer in a Neural Network. During this training, the network learns to assign similar vectors to words that have similar meanings or are used in similar contexts. The resulting parameterized embedding layer usually captures far more information about words and language than a simple one-to-one dictionary mapping.

We implement search by passing each sequence we want to be able to query through the embedding function/model and storing the calculated embedding vectors (one vector per embedded sequence). Then, we calculate the similarity between all the stored embeddings and our `query` string, and fetch results that result in a high similarity ranking. Similarity is usually calculated as a distance measure between the two vectors, for example the angle between the two multi-dimensional vectors: if the angle is 0 degrees, they are completely similar, if it's 90 degrees they are completely dissimilar.

## Sample Project Structure

Depending on the structure of the Flask app, there are subtle differences in how to implement the necessary parts. I use a blueprint-based structure, where the flask app is initialized in a factory module, so it goes like the following lines:

- app/
  - main/
    - \_\_init\_\_.py
    - routes.py
    - forms.py
  - auth/
    - routes.py
  - models.py
  - \_\_init\_\_.py
- app.py
- config.py

Here, the `app/__init__.py` file contains the factory initialization function `create_app` that is used by `app.py` to create the `app` variable and all related flask extensions.

```python
# app.py

# ...
app = create_app(os.getenv("FLASK_CONFIG") or "default")
# ...
```

```python
# app/__init__.py

# ...
def create_app(config_class='default'):
    app = Flask(__name__)
    app.config.from_object(config[config_class])

    from .main import bp as main_bp
    app.register_blueprint(main_bp)

    from .auth import auth as auth_blueprint 
    app.register_blueprint(auth_blueprint, url_prefix='/auth')

    # ...
    return app

# ...
```

## Implementation

### 1. ChromaDB initialization

We initialize the ChromaDB in the `app/__init__.py` file, and we make sure to specify a persistent directory for the calculated embedding vectors for each processed and stored text sequence.

```python
# app/__init__.py

# ... 
chroma = chromadb.Client(chromadbSettings(
        chroma_db_impl="duckdb+parquet",
        persist_directory="cache_chromadb",
        ))
# ... 
```

Note we are using a locally run Chroma implementation. Much like using an SQLite database instead of a client/server database, however, this is not an ideal scenario when one is looking to scale the app. ChromaDB supports a client/server implementation via a docker image.

### 2. ChromaDB collection management

We now need to define some functions that will manipulate the ChromaDB collection objects during our application's runtime.


Remember, as the implementation relates to the Journal Hub project, the search functionality is about searching for papers relevant to a full-text query, that have their respective SQLAlchemy models defined in `app/models.py`. Each model can have separate searchable attributes, defined via the `__searchable__` dunder attribute.

The approach is as modular as possible with respect to other `db.model`s, but there will be need for a few if/else checks within the functions to differentiate the handling for each model class.

```python
# app/models.py

# ... 
class PaperShowcase(db.Model):
    __searchable__ = ['source', 'identifier', 'secondary_identifier', 'abstract', 'title']
    __tablename__ = 'papers'
    id = db.Column(db.Integer, primary_key=True)
    identifier = db.Column(db.String(50), unique=True, index=True)
    secondary_identifier = db.Column(db.String(50), index=True)
    abstract = db.Column(db.String(10000))
    title = db.Column(db.String(10000))
    # ...

```


We create a new `app/search.py` file to contain these functions:

```python
from flask import current_app
from chromadb.utils import embedding_functions

def add_to_collection(collection, model):
    # collection builder for SQLalchemy model
    c = current_app.chromadb.get_or_create_collection(collection, embedding_function=embedding_functions.DefaultEmbeddingFunction())
    # searchable document is the concatenation of all relevant text fields
    entry = ""
    for field in model.__searchable__:
        if getattr(model, field) is not None:
            entry = entry + " " + getattr(model, field)
    metadatas = [{'source': getattr(model, 'identifier')+getattr(model,'secondary_identifier') if getattr(model,'secondary_identifier') is not None else getattr(model,'identifier')}]
    # note upsert instead of add
    c.upsert(documents=[entry],
                            metadatas=metadatas,
                            ids=[f"{collection}_{str(getattr(model, 'id'))}"])
    current_app.chromadb.persist() # needed?


def remove_from_collection(collection, model):
    try:
        c = current_app.chromadb.get_collection(collection, embedding_function=embedding_functions.DefaultEmbeddingFunction())
    except Exception as e:
        print(f"Could not find collection {collection} - {e}")    
    c.delete(ids=[getattr(model, 'id')])
    current_app.chromadb.persist() # needed?


def query_collection(collection, query_str):
    try:
        c = current_app.chromadb.get_collection(collection, embedding_function=embedding_functions.DefaultEmbeddingFunction())
    except Exception as e:
        print(f"Could not find collection {collection} - {e}")
    results = c.query(query_texts=[query_str])
    ids = [int(i.split(f"{collection}_")[1]) for i in results['ids'][0]] # for isinstance(query,str) you unpack list of lists in results
    scores = [float(i) for i in results['distances'][0]] # for isinstance(query,str) you unpack list of lists in results
    return ids, scores
```

In `add_to_collection`, we handle the logic for every occasion we want to embed some data stored under a `model` class in our ChromaDB `collection` object. We first create an entry to be embedded by concatenating all the searchable fields in the database row/instance. The metadata object required by ChromaDB requires a 'source' key-value pair, providing a reference source from the relevant `model.identifiers` (sometimes a `secondary_identifier` exists, but that's just some extra logic). Thus, the embedded information for a paper will be referenced in the source by the paper's identifier(s) in the database. The entry is then upserted in the collection, and the collection's `id` is the same as the database's `model.id`. The requisiteness of the `current_app.chromadb.persist()` call is not clear for me, but I added it for good measure. The `remove_from_collection` function just deletes an object from the collection.

When the `add_to_collection` is run for the first time, the default embeddings model will be downloaded and stored in a local cache directory.

The querying of the ChromaDB collection happens at `query_collection`, where there's a `query_str` as an argument. We call the `query()` method of the collection, and we retrieve a `results` dictionary. This contains `ids` and calculated similarity `distances`, as a list corresponding to our query string. A collection's `query()` method allows for a list of query strings, but in our case we provide a single one. We return the integer ids for each vector in the collection, along with the similarity scores calculated against our query. 


### 3. SQLALchemy Mixin

Now that we have references to the ids and the scores, we can interface with SQLAlchemy queries.

I hinted at a Mixin Class earlier, and this is where it gets into play. We basically want to create a class from which our `db.model`s will inherit a `search()` method from. We also need to handle automatic synchronization between the SQL database and ChromaDB, at insertion, modification and deletion time of to-be-queried paper data.

Here's the class:

```python
# app/models.py

# ... 

# searchable SQLalchemy mixin for generic searching functionality
class SearchableMixin(object):
    @classmethod
    def search(cls, expression, user, page=None, per_page=None):
        ids, scores = query_collection(cls.__tablename__, expression, page, per_page)
        if len(scores)==0:
            return cls.query.filter(False), []
        ranking = []
        # print(ids)
        for i in range(len(ids)):
            ranking.append((ids[i],i))
        results = db.session.query(PaperShowcase)\
            .filter(cls.id.in_(ids))\
            .order_by(db.case(*ranking, value=cls.id))
        return results, scores

    @classmethod
    def before_commit(cls, session):
        setattr(session, f"{cls.__tablename__}_changes", {
            'add': [obj for obj in session.new if isinstance(obj, cls)],
            'update': [obj for obj in session.dirty if isinstance(obj, cls)],
            'delete': [obj for obj in session.deleted if isinstance(obj, cls)],
        })

    @classmethod
    def after_commit(cls, session):
        session_idx_change = getattr(session, f"{cls.__tablename__}_changes")
        if session_idx_change:
            for obj in session_idx_change['add']:
                add_to_collection(cls.__tablename__, obj)
            for obj in session_idx_change['update']:
                add_to_collection(cls.__tablename__, obj)
            for obj in session_idx_change['delete']:
                remove_from_collection(cls.__tablename__, obj)
            setattr(session, f"{cls.__tablename__}_changes", None)
            current_app.chromadb.persist()

    @classmethod
    def reindex(cls):
        for obj in cls.query:
            add_to_collection(cls.__tablename__, obj)

# ...
```

For the `search` method, we get `ids` and `scores` from the `query_collection` function introduced previously in the `app/search.py` module. The rest is a procedure to use the `ids` as filters in a SQLAlchemy query. For this, we create a ranking list of tuples, that we can use in the `order_by` method. This way, we receive SQL query results based on the similarity score. An edge case for 0 scores returned is also handled, corresponding basically to an empty database as this implementation should return something no matter how small the similarity score is.

The `before_commit` and `after_commit` class methods are defined so that they perform the necessary manipulations based on session-level changes. Note that the `session` object here is a `db.session`, not Flask's `session` cookie storage. We use these methods in SQLAlchemy listeners created at the end of the `app/models.py` file:

```python
# app/models.py

# ...

db.event.listen(db.session, 'before_commit', PaperShowcase.before_commit)
db.event.listen(db.session, 'after_commit', PaperShowcase.after_commit)
```

We also implement a `reindex()` class method, to be used when an empty ChromaDB needs to be re-populated based on our relational database.

### 4. Search endpoint route

The final piece in this puzzle is the definition of an endpoint to handle the search requests. As done in Grinberg's post, I assume a `GET`-capable search form in the navbar (accessible from all routes, via flask's `g` global storage):

```python
# app/main/routes.py

# ...
@main.before_app_request
def before_request():
    g.search_form = SearchNavbarForm()
# ...
```

and now we can handle this with `GET` requests:

```python
# app/main/routes.py

# ...
@main.route('/search')
def search():
    if not g.search_form.validate():
        print(g.search_form.errors)
        return redirect(url_for('main.index'))
    results, scores = PaperShowcase.search(g.search_form.q.data, current_user)
    results = [i.to_dict() for i in results]
    return render_template('showcases/search.html', 
                           type="papers",
                           query=g.search_form.q.data, 
                           results=results, 
                           scores=scores)
# ...
```

Here, the `to_dict()` is a helper instance method for the `PaperShowcase` model, allowing us to convert to JSON on the jinja frontend to use with javascript components. Similar handling could of course happen without converting from SQLAlchemy objects if there's no such requirement.

## Wrap-up

Et voila! You have implemented full-text search functionality using modern text-embedding models! 

Here's how it works in the Journal Hub app:

<div class="rounded-full">
    <img class="m-auto rounded-lg" src="{{site.baseurl}}/assets/gif/Journal_Hub_search.gif">
</div>

As a reminder, note that to scale your development, you need to reconsider the local `duckdb+parquet` implementation of ChromaDB and go to a client/server implementation. If you don't, I've had inconsistencies and bugs pop-up even when using a gunicorn production server with many worker threads.
